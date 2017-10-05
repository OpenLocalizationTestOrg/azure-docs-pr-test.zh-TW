---
title: "Azure Active Directory v2.0 範圍、權限及同意 | Microsoft Docs"
description: "Azure AD v2.0 端點中的授權說明，包括範圍、權限及同意。"
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
ms.openlocfilehash: 04869a7627ecb3e6a0d11733fae7da2ecb04ed51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scopes-permissions-and-consent-in-the-azure-active-directory-v20-endpoint"></a><span data-ttu-id="24c1d-103">Azure Active Directory v2.0 端點中的範圍、權限及同意</span><span class="sxs-lookup"><span data-stu-id="24c1d-103">Scopes, permissions, and consent in the Azure Active Directory v2.0 endpoint</span></span>
<span data-ttu-id="24c1d-104">與 Azure Active Directory (Azure AD) 整合的應用程式會遵循一種授權模型，可讓使用者控制應用程式存取他們資料的方式。</span><span class="sxs-lookup"><span data-stu-id="24c1d-104">Apps that integrate with Azure Active Directory (Azure AD) follow an authorization model that gives users control over how an app can access their data.</span></span> <span data-ttu-id="24c1d-105">v2.0 的授權模型實作已更新，它變更了應用程式必須與 Azure AD 互動的方式。</span><span class="sxs-lookup"><span data-stu-id="24c1d-105">The v2.0 implementation of the authorization model has been updated, and it changes how an app must interact with Azure AD.</span></span> <span data-ttu-id="24c1d-106">本文涵蓋此授權模型的基本概念，包括範圍、權限及同意。</span><span class="sxs-lookup"><span data-stu-id="24c1d-106">This article covers the basic concepts of this authorization model, including scopes, permissions, and consent.</span></span>

> [!NOTE]
> <span data-ttu-id="24c1d-107">v2.0 端點並未支援所有的 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="24c1d-107">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span> <span data-ttu-id="24c1d-108">若要判斷您是否應該使用 v2.0 端點，請參閱 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-108">To determine whether you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
>
>

## <a name="scopes-and-permissions"></a><span data-ttu-id="24c1d-109">範圍和權限</span><span class="sxs-lookup"><span data-stu-id="24c1d-109">Scopes and permissions</span></span>
<span data-ttu-id="24c1d-110">Azure AD 實作 [OAuth 2.0](active-directory-v2-protocols.md) 授權通訊協定。</span><span class="sxs-lookup"><span data-stu-id="24c1d-110">Azure AD implements the [OAuth 2.0](active-directory-v2-protocols.md) authorization protocol.</span></span> <span data-ttu-id="24c1d-111">OAuth 2.0 是一種可讓協力廠商應用程式代表使用者存取 Web 主控資源的方法。</span><span class="sxs-lookup"><span data-stu-id="24c1d-111">OAuth 2.0 is a method through which a third-party app can access web-hosted resources on behalf of a user.</span></span> <span data-ttu-id="24c1d-112">任何與 Azure AD 整合的 Web 主控資源都具有資源識別碼 (或稱「應用程式識別碼 URI」)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-112">Any web-hosted resource that integrates with Azure AD has a resource identifier, or *Application ID URI*.</span></span> <span data-ttu-id="24c1d-113">例如，Microsoft 的 Web 主控資源包括：</span><span class="sxs-lookup"><span data-stu-id="24c1d-113">For example, some of Microsoft's web-hosted resources include:</span></span>

* <span data-ttu-id="24c1d-114">Office 365 整合郵件 API： `https://outlook.office.com`</span><span class="sxs-lookup"><span data-stu-id="24c1d-114">The Office 365 Unified Mail API: `https://outlook.office.com`</span></span>
* <span data-ttu-id="24c1d-115">Azure AD Graph API： `https://graph.windows.net`</span><span class="sxs-lookup"><span data-stu-id="24c1d-115">The Azure AD Graph API: `https://graph.windows.net`</span></span>
* <span data-ttu-id="24c1d-116">Microsoft Graph：`https://graph.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="24c1d-116">Microsoft Graph: `https://graph.microsoft.com`</span></span>

<span data-ttu-id="24c1d-117">這也適用於已與 Azure AD 整合的任何協力廠商資源。</span><span class="sxs-lookup"><span data-stu-id="24c1d-117">The same is true for any third-party resources that have integrated with Azure AD.</span></span> <span data-ttu-id="24c1d-118">任何這些資源也都可以定義一組權限，可用來進一步細分該資源的功能。</span><span class="sxs-lookup"><span data-stu-id="24c1d-118">Any of these resources also can define a set of permissions that can be used to divide the functionality of that resource into smaller chunks.</span></span> <span data-ttu-id="24c1d-119">例如，[Microsoft Graph](https://graph.microsoft.io) 除了別的之外，還定義了權限來執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="24c1d-119">As an example, [Microsoft Graph](https://graph.microsoft.io) has defined permissions to do the following tasks, among others:</span></span>

* <span data-ttu-id="24c1d-120">讀取使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="24c1d-120">Read a user's calendar</span></span>
* <span data-ttu-id="24c1d-121">寫入使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="24c1d-121">Write to a user's calendar</span></span>
* <span data-ttu-id="24c1d-122">以使用者身分傳送郵件</span><span class="sxs-lookup"><span data-stu-id="24c1d-122">Send mail as a user</span></span>

<span data-ttu-id="24c1d-123">藉由定義這些類型的權限，資源可以更精細地掌控其資料及資料的公開方式。</span><span class="sxs-lookup"><span data-stu-id="24c1d-123">By defining these types of permissions, the resource has fine-grained control over its data and how the data is exposed.</span></span> <span data-ttu-id="24c1d-124">協力廠商應用程式可以向應用程式使用者要求這些權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-124">A third-party app can request these permissions from an app user.</span></span> <span data-ttu-id="24c1d-125">應用程式使用者必須先核准權限，應用程式才能代表使用者執行動作。</span><span class="sxs-lookup"><span data-stu-id="24c1d-125">The app user must approve the permissions before the app can act on the user's behalf.</span></span> <span data-ttu-id="24c1d-126">透過將資源的功能切割成較小的權限集，便可將協力廠商應用程式建置成只要求它們執行其功能所需的特定權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-126">By chunking the resource's functionality into smaller permission sets, third-party apps can be built to request only the specific permissions that they need to perform their function.</span></span> <span data-ttu-id="24c1d-127">應用程式使用者會確切知道應用程式將如何使用其資料，因而能夠更確信應用程式的行為不具惡意企圖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-127">App users can know exactly how an app will use their data, and they can be more confident that the app is not behaving with malicious intent.</span></span>

<span data-ttu-id="24c1d-128">在 Azure AD 和 OAuth 中，這些類型的權限也稱為「範圍」。</span><span class="sxs-lookup"><span data-stu-id="24c1d-128">In Azure AD and OAuth, these types of permissions are called *scopes*.</span></span> <span data-ttu-id="24c1d-129">它們有時也稱為 *oAuth2Permissions*。</span><span class="sxs-lookup"><span data-stu-id="24c1d-129">They also sometimes are referred to as *oAuth2Permissions*.</span></span> <span data-ttu-id="24c1d-130">在 Azure AD 中範圍會以字串值表示。</span><span class="sxs-lookup"><span data-stu-id="24c1d-130">A scope is represented in Azure AD as a string value.</span></span> <span data-ttu-id="24c1d-131">繼續討論 Microsoft Graph 範例，每個權限的範圍值如下：</span><span class="sxs-lookup"><span data-stu-id="24c1d-131">Continuing with the Microsoft Graph example, the scope value for each permission is:</span></span>

* <span data-ttu-id="24c1d-132">使用 `Calendar.Read` 來讀取使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="24c1d-132">Read a user's calendar by using `Calendar.Read`</span></span>
* <span data-ttu-id="24c1d-133">使用 `Mail.ReadWrite` 來寫入使用者的行事曆</span><span class="sxs-lookup"><span data-stu-id="24c1d-133">Write to a user's calendar by using `Mail.ReadWrite`</span></span>
* <span data-ttu-id="24c1d-134">使用 `Mail.Send` 來以使用者身分傳送郵件</span><span class="sxs-lookup"><span data-stu-id="24c1d-134">Send mail as a user using by `Mail.Send`</span></span>

<span data-ttu-id="24c1d-135">透過在對 v2.0 端點的要求中指定範圍，應用程式便可要求這些權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-135">An app can request these permissions by specifying the scopes in requests to the v2.0 endpoint.</span></span>

## <a name="openid-connect-scopes"></a><span data-ttu-id="24c1d-136">OpenId Connect 範圍</span><span class="sxs-lookup"><span data-stu-id="24c1d-136">OpenID Connect scopes</span></span>
<span data-ttu-id="24c1d-137">v2.0 的 OpenID Connect 實作有一些定義妥善但不會套用至特定資源的範圍：`openid`、`email`、`profile` 和 `offline_access`。</span><span class="sxs-lookup"><span data-stu-id="24c1d-137">The v2.0 implementation of OpenID Connect has a few well-defined scopes that do not apply to a specific resource: `openid`, `email`, `profile`, and `offline_access`.</span></span>

### <a name="openid"></a><span data-ttu-id="24c1d-138">openid</span><span class="sxs-lookup"><span data-stu-id="24c1d-138">openid</span></span>
<span data-ttu-id="24c1d-139">如果應用程式使用 [OpenID Connect](active-directory-v2-protocols.md) 來執行登入，它就必須要求 `openid` 範圍。</span><span class="sxs-lookup"><span data-stu-id="24c1d-139">If an app performs sign-in by using [OpenID Connect](active-directory-v2-protocols.md), it must request the `openid` scope.</span></span> <span data-ttu-id="24c1d-140">`openid` 範圍會在工作帳戶同意頁面上顯示為「將您登入」權限，而在個人 Microsoft 帳戶同意頁面上會顯示為「檢視您的設定檔並使用您的 Microsoft 帳戶連接到應用程式和服務」權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-140">The `openid` scope shows on the work account consent page as the "Sign you in" permission, and on the personal Microsoft account consent page as the "View your profile and connect to apps and services using your Microsoft account" permission.</span></span> <span data-ttu-id="24c1d-141">有了此權限之後，應用程式便能夠以 `sub` 宣告的形式接收使用者的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="24c1d-141">With this permission, an app can receive a unique identifier for the user in the form of the `sub` claim.</span></span> <span data-ttu-id="24c1d-142">它也會為應用程式提供 UserInfo 端點的存取權。</span><span class="sxs-lookup"><span data-stu-id="24c1d-142">It also gives the app access to the UserInfo endpoint.</span></span> <span data-ttu-id="24c1d-143">`openid` 範圍也可在 v2.0 權杖端點用來取得識別碼權杖，而該權杖可用來保護應用程式不同元件之間的 HTTP 呼叫。</span><span class="sxs-lookup"><span data-stu-id="24c1d-143">The `openid` scope can be used at the v2.0 token endpoint to acquire ID tokens, which can be used to secure HTTP calls between different components of an app.</span></span>

### <a name="email"></a><span data-ttu-id="24c1d-144">電子郵件</span><span class="sxs-lookup"><span data-stu-id="24c1d-144">email</span></span>
<span data-ttu-id="24c1d-145">`email` 範圍可以與 `openid` 範圍及任何其他範圍搭配使用。</span><span class="sxs-lookup"><span data-stu-id="24c1d-145">The `email` scope can be used with the `openid` scope and any others.</span></span> <span data-ttu-id="24c1d-146">它會以 `email` 宣告的形式為應用程式提供使用者主要電子郵件地址的存取權。</span><span class="sxs-lookup"><span data-stu-id="24c1d-146">It gives the app access to the user's primary email address in the form of the `email` claim.</span></span> <span data-ttu-id="24c1d-147">只有當電子郵件地址與使用者帳戶關聯 (兩者並不一定會關聯) 時，`email` 宣告才會包含在權杖中。</span><span class="sxs-lookup"><span data-stu-id="24c1d-147">The `email` claim is included in a token only if an email address is associated with the user account, which is not always the case.</span></span> <span data-ttu-id="24c1d-148">如果它使用 `email` 範圍，您的應用程式就應該做好準備，以處理權杖中沒有 `email` 宣告的情況。</span><span class="sxs-lookup"><span data-stu-id="24c1d-148">If it uses the `email` scope, your app should be prepared to handle a case in which the `email` claim does not exist in the token.</span></span>

### <a name="profile"></a><span data-ttu-id="24c1d-149">設定檔</span><span class="sxs-lookup"><span data-stu-id="24c1d-149">profile</span></span>
<span data-ttu-id="24c1d-150">`profile` 範圍可以與 `openid` 範圍及任何其他範圍搭配使用。</span><span class="sxs-lookup"><span data-stu-id="24c1d-150">The `profile` scope can be used with the `openid` scope and any others.</span></span> <span data-ttu-id="24c1d-151">它會為應用程式提供大量使用者相關資訊的存取權。</span><span class="sxs-lookup"><span data-stu-id="24c1d-151">It gives the app access to a substantial amount of information about the user.</span></span> <span data-ttu-id="24c1d-152">它能存取的資訊包括但不限於使用者的名字、姓氏、慣用使用者名稱及物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="24c1d-152">The information it can access includes, but is not limited to, the user's given name, surname, preferred username, and object ID.</span></span> <span data-ttu-id="24c1d-153">如需特定使用者之識別碼權杖中可用的設定檔宣告完整清單，請參閱 [v2.0 權杖參考](active-directory-v2-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-153">For a complete list of the profile claims available in the id_tokens parameter for a specific user, see the [v2.0 tokens reference](active-directory-v2-tokens.md).</span></span>

### <a name="offlineaccess"></a><span data-ttu-id="24c1d-154">offline_access</span><span class="sxs-lookup"><span data-stu-id="24c1d-154">offline_access</span></span>
<span data-ttu-id="24c1d-155">[`offline_access` 範圍](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess)可延長您應用程式代表使用者存取資源的時間。</span><span class="sxs-lookup"><span data-stu-id="24c1d-155">The [`offline_access` scope](http://openid.net/specs/openid-connect-core-1_0.html#OfflineAccess) gives your app access to resources on behalf of the user for an extended time.</span></span> <span data-ttu-id="24c1d-156">在工作帳戶同意畫面上，此範圍會顯示為「隨時存取您的資料」權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-156">On the work account consent page, this scope appears as the "Access your data anytime" permission.</span></span> <span data-ttu-id="24c1d-157">在個人 Microsoft 帳戶同意頁面上，它會顯示為「隨時存取您的資訊」權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-157">On the personal Microsoft account consent page, it appears as the "Access your info anytime" permission.</span></span> <span data-ttu-id="24c1d-158">當使用者核准 `offline_access` 範圍時，您的應用程式將可從 v2.0 權杖端點收到重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-158">When a user approves the `offline_access` scope, your app can receive refresh tokens from the v2.0 token endpoint.</span></span> <span data-ttu-id="24c1d-159">重新整理權杖是長期權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-159">Refresh tokens are long-lived.</span></span> <span data-ttu-id="24c1d-160">您的應用程式可以在舊存取權杖到期時取得新的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-160">Your app can get new access tokens as older ones expire.</span></span>

<span data-ttu-id="24c1d-161">如果您的應用程式未要求 `offline_access` 範圍，則不會收到重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-161">If your app does not request the `offline_access` scope, it won't receive refresh tokens.</span></span> <span data-ttu-id="24c1d-162">這意謂著當您在 [OAuth 2.0 授權碼流程](active-directory-v2-protocols.md)中兌換授權碼時，您只會從 `/token` 端點收到存取權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-162">This means that when you redeem an authorization code in the [OAuth 2.0 authorization code flow](active-directory-v2-protocols.md), you'll receive only an access token from the `/token` endpoint.</span></span> <span data-ttu-id="24c1d-163">存取權杖的有效期短。</span><span class="sxs-lookup"><span data-stu-id="24c1d-163">The access token is valid for a short time.</span></span> <span data-ttu-id="24c1d-164">存取權杖的有效期通常在一小時內。</span><span class="sxs-lookup"><span data-stu-id="24c1d-164">The access token usually expires in one hour.</span></span> <span data-ttu-id="24c1d-165">屆時，您的應用程式將必須把使用者重新導向回 `/authorize` 端點，以擷取新的授權碼。</span><span class="sxs-lookup"><span data-stu-id="24c1d-165">At that point, your app needs to redirect the user back to the `/authorize` endpoint to get a new authorization code.</span></span> <span data-ttu-id="24c1d-166">在此重新導向期間，視應用程式的類型而定，使用者可能需要重新輸入其認證或重新同意權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-166">During this redirect, depending on the type of app, the user might need to enter their credentials again or consent again to permissions.</span></span>

<span data-ttu-id="24c1d-167">如需有關如何取得及使用重新整理權杖的詳細資訊，請參閱 [v2.0 通訊協定參考](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-167">For more information about how to get and use refresh tokens, see the [v2.0 protocol reference](active-directory-v2-protocols.md).</span></span>

## <a name="requesting-individual-user-consent"></a><span data-ttu-id="24c1d-168">要求個別使用者同意</span><span class="sxs-lookup"><span data-stu-id="24c1d-168">Requesting individual user consent</span></span>
<span data-ttu-id="24c1d-169">在 [OpenID Connect 或 OAuth 2.0](active-directory-v2-protocols.md) 授權要求中，應用程式可以使用 `scope` 查詢參數來要求它所需的權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-169">In an [OpenID Connect or OAuth 2.0](active-directory-v2-protocols.md) authorization request, an app can request the permissions it needs by using the `scope` query parameter.</span></span> <span data-ttu-id="24c1d-170">例如，當使用者登入應用程式時，應用程式會傳送如以下範例的要求 (加入分行符號是為了增加可讀性)：</span><span class="sxs-lookup"><span data-stu-id="24c1d-170">For example, when a user signs in to an app, the app sends a request like the following example (with line breaks added for legibility):</span></span>

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

<span data-ttu-id="24c1d-171">`scope` 參數是應用程式所要求的範圍清單 (以空格分隔)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-171">The `scope` parameter is a space-separated list of scopes that the app is requesting.</span></span> <span data-ttu-id="24c1d-172">藉由在資源的識別碼 (應用程式識別碼 URI) 附加範圍值，即可指出每個範圍。</span><span class="sxs-lookup"><span data-stu-id="24c1d-172">Each scope is indicated by appending the scope value to the resource's identifier (the Application ID URI).</span></span> <span data-ttu-id="24c1d-173">在要求範例中，應用程式需要權限來讀取使用者的行事曆，以及以使用者身分傳送郵件。</span><span class="sxs-lookup"><span data-stu-id="24c1d-173">In the request example, the app needs permission to read the user's calendar and send mail as the user.</span></span>

<span data-ttu-id="24c1d-174">在使用者輸入其認證之後，v2.0 端點會檢查是否有相符的 「使用者同意」記錄。</span><span class="sxs-lookup"><span data-stu-id="24c1d-174">After the user enters their credentials, the v2.0 endpoint checks for a matching record of *user consent*.</span></span> <span data-ttu-id="24c1d-175">如果使用者過去未曾對所要求的任何權限表示同意，v2.0 端點就會要求使用者授與所要求的權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-175">If the user has not consented to any of the requested permissions in the past, the v2.0 endpoint asks the user to grant the requested permissions.</span></span>

![工作帳戶同意](../../media/active-directory-v2-flows/work_account_consent.png)

<span data-ttu-id="24c1d-177">當使用者核准權限時，系統就會記錄同意，讓使用者在後續登入時不需要重新表示同意。</span><span class="sxs-lookup"><span data-stu-id="24c1d-177">When the user approves the permission, the consent is recorded so that the user doesn't have to consent again on subsequent account sign-ins.</span></span>

## <a name="requesting-consent-for-an-entire-tenant"></a><span data-ttu-id="24c1d-178">要求整個租用戶的同意</span><span class="sxs-lookup"><span data-stu-id="24c1d-178">Requesting consent for an entire tenant</span></span>
<span data-ttu-id="24c1d-179">通常，當組織購買某個應用程式的授權或訂用帳戶時，會想要為其員工完整佈建應用程式。</span><span class="sxs-lookup"><span data-stu-id="24c1d-179">Often, when an organization purchases a license or subscription for an application, the organization wants to fully provision the application for its employees.</span></span> <span data-ttu-id="24c1d-180">在此過程中，系統管理員可以授與同意，讓應用程式代表任何員工進行動作。</span><span class="sxs-lookup"><span data-stu-id="24c1d-180">As part of this process, an administrator can grant consent for the application to act on behalf of any employee.</span></span> <span data-ttu-id="24c1d-181">如果系統管理員為整個租用戶授與同意，該組織的員工便不會看見應用程式的同意頁面。</span><span class="sxs-lookup"><span data-stu-id="24c1d-181">If the admin grants consent for the entire tenant, the organization's employees won't see a consent page for the application.</span></span>

<span data-ttu-id="24c1d-182">若要針對租用戶中的所有使用者要求同意，您的應用程式可以使用系統管理員同意端點。</span><span class="sxs-lookup"><span data-stu-id="24c1d-182">To request consent for all users in a tenant, your app can use the admin consent endpoint.</span></span>

## <a name="admin-restricted-scopes"></a><span data-ttu-id="24c1d-183">受系統管理員限制的範圍</span><span class="sxs-lookup"><span data-stu-id="24c1d-183">Admin-restricted scopes</span></span>
<span data-ttu-id="24c1d-184">Microsoft 生態系統中的某些高特權權限可以設定為「受系統管理員限制」。</span><span class="sxs-lookup"><span data-stu-id="24c1d-184">Some high-privilege permissions in the Microsoft ecosystem can be set to *admin-restricted*.</span></span> <span data-ttu-id="24c1d-185">這類範圍的範例包括下列權限：</span><span class="sxs-lookup"><span data-stu-id="24c1d-185">Examples of these kinds of scopes include the following permissions:</span></span>

* <span data-ttu-id="24c1d-186">使用 `Directory.Read` 來讀取組織的目錄資料</span><span class="sxs-lookup"><span data-stu-id="24c1d-186">Read an organization's directory data by using `Directory.Read`</span></span>
* <span data-ttu-id="24c1d-187">使用 `Directory.ReadWrite` 將資料寫入組織的目錄</span><span class="sxs-lookup"><span data-stu-id="24c1d-187">Write data to an organization's directory by using `Directory.ReadWrite`</span></span>
* <span data-ttu-id="24c1d-188">使用 `Groups.Read.All` 來讀取組織目錄中的安全性群組</span><span class="sxs-lookup"><span data-stu-id="24c1d-188">Read security groups in an organization's directory by using `Groups.Read.All`</span></span>

<span data-ttu-id="24c1d-189">雖然取用者使用者可以為應用程式授與這類資料的存取權，但組織使用者會受到限制，而無法授與同一組機密公司資料的存取權。</span><span class="sxs-lookup"><span data-stu-id="24c1d-189">Although a consumer user might grant an application access to this kind of data, organizational users are restricted from granting access to the same set of sensitive company data.</span></span> <span data-ttu-id="24c1d-190">如果您的應用程式向組織使用者要求這其中一個權限的存取權，使用者將會收到錯誤訊息，指出他們未獲授權而無法對您應用程式的權限表示同意。</span><span class="sxs-lookup"><span data-stu-id="24c1d-190">If your application requests access to one of these permissions from an organizational user, the user receives an error message that says they are not authorized to consent to your app's permissions.</span></span>

<span data-ttu-id="24c1d-191">如果您的應用程式需要存取組織的受系統管理員限制範圍，您應該同樣使用系統管理員同意端點，直接向公司系統管理員要求權限，接下來將會說明。</span><span class="sxs-lookup"><span data-stu-id="24c1d-191">If your app requires access to admin-restricted scopes for organizations, you should request them directly from a company administrator, also by using the admin consent endpoint, described next.</span></span>

<span data-ttu-id="24c1d-192">當系統管理員透過系統管理員同意端點授與這些權限時，會針對租用戶中所有的使用者授與同意。</span><span class="sxs-lookup"><span data-stu-id="24c1d-192">When an administrator grants these permissions via the admin consent endpoint, consent is granted for all users in the tenant.</span></span>

## <a name="using-the-admin-consent-endpoint"></a><span data-ttu-id="24c1d-193">使用系統管理員同意端點</span><span class="sxs-lookup"><span data-stu-id="24c1d-193">Using the admin consent endpoint</span></span>
<span data-ttu-id="24c1d-194">如果您依照這些步驟，您的應用程式便能針對租用戶中所有的使用者收集權限，包括受系統管理員限制的範圍。</span><span class="sxs-lookup"><span data-stu-id="24c1d-194">If you follow these steps, your app can gather permissions for all users in a tenant, including admin-restricted scopes.</span></span> <span data-ttu-id="24c1d-195">若要查看實作這些步驟的程式碼範例，請參閱[受系統管理員限制的範圍範例](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-195">To see a code sample that implements the steps, see the [admin-restricted scopes sample](https://github.com/Azure-Samples/active-directory-dotnet-admin-restricted-scopes-v2).</span></span>

### <a name="request-the-permissions-in-the-app-registration-portal"></a><span data-ttu-id="24c1d-196">在應用程式註冊入口網站中要求權限</span><span class="sxs-lookup"><span data-stu-id="24c1d-196">Request the permissions in the app registration portal</span></span>
1. <span data-ttu-id="24c1d-197">在[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)中移至您的應用程式，或[建立應用程式](active-directory-v2-app-registration.md) (如果您尚未這麼做)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-197">Go to your application in the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or [create an app](active-directory-v2-app-registration.md) if you haven't already.</span></span>
2. <span data-ttu-id="24c1d-198">找出 [Microsoft Graph 權限] 區段，然後新增您應用程式所需的權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-198">Locate the **Microsoft Graph Permissions** section, and then add the permissions that your app requires.</span></span>
3. <span data-ttu-id="24c1d-199">確定 [儲存] 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="24c1d-199">Make sure you **Save** the app registration.</span></span>

### <a name="recommended-sign-the-user-in-to-your-app"></a><span data-ttu-id="24c1d-200">建議︰將使用者登入您的應用程式</span><span class="sxs-lookup"><span data-stu-id="24c1d-200">Recommended: Sign the user in to your app</span></span>
<span data-ttu-id="24c1d-201">通常，當您建置使用系統管理員同意端點的應用程式時，應用程式會需要一個可供系統管理員核准應用程式權限的頁面或檢視。</span><span class="sxs-lookup"><span data-stu-id="24c1d-201">Typically, when you build an application that uses the admin consent endpoint, the app needs a page or view in which the admin can approve the app's permissions.</span></span> <span data-ttu-id="24c1d-202">此頁面可以是應用程式註冊流程的一部分、應用程式設定的一部分，或是專用的「連接」流程。</span><span class="sxs-lookup"><span data-stu-id="24c1d-202">This page can be part of the app's sign-up flow, part of the app's settings, or it can be a dedicated "connect" flow.</span></span> <span data-ttu-id="24c1d-203">在許多情況下，應用程式只在使用者利用工作或學校 Microsoft 帳戶登入之後顯示此「連接」檢視是很合理的。</span><span class="sxs-lookup"><span data-stu-id="24c1d-203">In many cases, it makes sense for the app to show this "connect" view only after a user has signed in with a work or school Microsoft account.</span></span>

<span data-ttu-id="24c1d-204">將使用者登入應用程式時，您可以先識別系統管理員所屬的組織，然後再要求他們核准必要的權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-204">When you sign the user in to your app, you can identify the organization to which the admin belongs before asking them to approve the necessary permissions.</span></span> <span data-ttu-id="24c1d-205">雖然這並非絕對必要，但這麼做可協助您為組織使用者建立更直覺式的體驗。</span><span class="sxs-lookup"><span data-stu-id="24c1d-205">Although not strictly necessary, it can help you create a more intuitive experience for your organizational users.</span></span> <span data-ttu-id="24c1d-206">若要讓使用者登入，請遵循我們的 [v2.0 通訊協定教學課程](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-206">To sign the user in, follow our [v2.0 protocol tutorials](active-directory-v2-protocols.md).</span></span>

### <a name="request-the-permissions-from-a-directory-admin"></a><span data-ttu-id="24c1d-207">向目錄管理員要求權限</span><span class="sxs-lookup"><span data-stu-id="24c1d-207">Request the permissions from a directory admin</span></span>
<span data-ttu-id="24c1d-208">當您已準備好向組織的系統管理員要求權限時，您可以將使用者重新導向到 v2.0「系統管理員同意端點」。</span><span class="sxs-lookup"><span data-stu-id="24c1d-208">When you're ready to request permissions from your organization's admin, you can redirect the user to the v2.0 *admin consent endpoint*.</span></span>

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting the below request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| <span data-ttu-id="24c1d-209">參數</span><span class="sxs-lookup"><span data-stu-id="24c1d-209">Parameter</span></span> | <span data-ttu-id="24c1d-210">條件</span><span class="sxs-lookup"><span data-stu-id="24c1d-210">Condition</span></span> | <span data-ttu-id="24c1d-211">說明</span><span class="sxs-lookup"><span data-stu-id="24c1d-211">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24c1d-212">tenant</span><span class="sxs-lookup"><span data-stu-id="24c1d-212">tenant</span></span> |<span data-ttu-id="24c1d-213">必要</span><span class="sxs-lookup"><span data-stu-id="24c1d-213">Required</span></span> |<span data-ttu-id="24c1d-214">您想要要求權限的目錄租用戶。</span><span class="sxs-lookup"><span data-stu-id="24c1d-214">The directory tenant that you want to request permission from.</span></span> <span data-ttu-id="24c1d-215">可以採用 GUID 或易記名稱格式。</span><span class="sxs-lookup"><span data-stu-id="24c1d-215">Can be provided in GUID or friendly name format.</span></span> |
| <span data-ttu-id="24c1d-216">client_id</span><span class="sxs-lookup"><span data-stu-id="24c1d-216">client_id</span></span> |<span data-ttu-id="24c1d-217">必要</span><span class="sxs-lookup"><span data-stu-id="24c1d-217">Required</span></span> |<span data-ttu-id="24c1d-218">[應用程式註冊入口網站](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)指派給您應用程式的「應用程式識別碼」。</span><span class="sxs-lookup"><span data-stu-id="24c1d-218">The Application ID that the [Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) assigned to your app.</span></span> |
| <span data-ttu-id="24c1d-219">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="24c1d-219">redirect_uri</span></span> |<span data-ttu-id="24c1d-220">必要</span><span class="sxs-lookup"><span data-stu-id="24c1d-220">Required</span></span> |<span data-ttu-id="24c1d-221">您想要傳送回應以供應用程式處理的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="24c1d-221">The redirect URI where you want the response to be sent for your app to handle.</span></span> <span data-ttu-id="24c1d-222">它必須與您在應用程式註冊入口網站中註冊的其中一個重新導向 URI 完全相符。</span><span class="sxs-lookup"><span data-stu-id="24c1d-222">It must exactly match one of the redirect URIs that you registered in the app registration portal.</span></span> |
| <span data-ttu-id="24c1d-223">state</span><span class="sxs-lookup"><span data-stu-id="24c1d-223">state</span></span> |<span data-ttu-id="24c1d-224">建議</span><span class="sxs-lookup"><span data-stu-id="24c1d-224">Recommended</span></span> |<span data-ttu-id="24c1d-225">同樣會隨權杖回應傳回之要求中所包含的值。</span><span class="sxs-lookup"><span data-stu-id="24c1d-225">A value included in the request that will also be returned in the token response.</span></span> <span data-ttu-id="24c1d-226">它可以是您想要的任何內容的字串。</span><span class="sxs-lookup"><span data-stu-id="24c1d-226">It can be a string of any content you want.</span></span> <span data-ttu-id="24c1d-227">請在驗證要求出現之前，先使用此狀態在應用程式中將使用者狀態的相關資訊 (例如他們之前所在的網頁或檢視) 編碼。</span><span class="sxs-lookup"><span data-stu-id="24c1d-227">Use the state to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span></span> |

<span data-ttu-id="24c1d-228">此時，Azure AD 會要求租用戶系統管理員登入來完成要求。</span><span class="sxs-lookup"><span data-stu-id="24c1d-228">At this point, Azure AD requires a tenant administrator to sign in to complete the request.</span></span> <span data-ttu-id="24c1d-229">系統會請系統管理員核准您在應用程式註冊入口網站中，為您應用程式要求的所有權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-229">The administrator is asked to approve all the permissions that you have requested for your app in the app registration portal.</span></span>

#### <a name="successful-response"></a><span data-ttu-id="24c1d-230">成功回應</span><span class="sxs-lookup"><span data-stu-id="24c1d-230">Successful response</span></span>
<span data-ttu-id="24c1d-231">如果系統管理員為您的應用程式核准權限，則成功的回應看起來會像這樣︰</span><span class="sxs-lookup"><span data-stu-id="24c1d-231">If the admin approves the permissions for your app, the successful response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| <span data-ttu-id="24c1d-232">參數</span><span class="sxs-lookup"><span data-stu-id="24c1d-232">Parameter</span></span> | <span data-ttu-id="24c1d-233">說明</span><span class="sxs-lookup"><span data-stu-id="24c1d-233">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24c1d-234">tenant</span><span class="sxs-lookup"><span data-stu-id="24c1d-234">tenant</span></span> |<span data-ttu-id="24c1d-235">將應用程式所要求的權限授與應用程式的目錄租用戶 (採用 GUID 格式)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-235">The directory tenant that granted your application the permissions it requested, in GUID format.</span></span> |
| <span data-ttu-id="24c1d-236">state</span><span class="sxs-lookup"><span data-stu-id="24c1d-236">state</span></span> |<span data-ttu-id="24c1d-237">一個包含在要求中而將一併在權杖回應中傳回的值。</span><span class="sxs-lookup"><span data-stu-id="24c1d-237">A value included in the request that also will be returned in the token response.</span></span> <span data-ttu-id="24c1d-238">它可以是您想要的任何內容的字串。</span><span class="sxs-lookup"><span data-stu-id="24c1d-238">It can be a string of any content you want.</span></span> <span data-ttu-id="24c1d-239">此狀態用於在驗證要求出現之前，於應用程式中編碼使用者的狀態資訊，例如之前所在的網頁或檢視。</span><span class="sxs-lookup"><span data-stu-id="24c1d-239">The state is used to encode information about the user's state in the app before the authentication request occurred, such as the page or view they were on.</span></span> |
| <span data-ttu-id="24c1d-240">admin_consent</span><span class="sxs-lookup"><span data-stu-id="24c1d-240">admin_consent</span></span> |<span data-ttu-id="24c1d-241">將設定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="24c1d-241">Will be set to **true**.</span></span> |

#### <a name="error-response"></a><span data-ttu-id="24c1d-242">錯誤回應</span><span class="sxs-lookup"><span data-stu-id="24c1d-242">Error response</span></span>
<span data-ttu-id="24c1d-243">如果系統管理員沒有為您的應用程式核准權限，則失敗的回應看起來會像這樣︰</span><span class="sxs-lookup"><span data-stu-id="24c1d-243">If the admin does not approve the permissions for your app, the failed response looks like this:</span></span>

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| <span data-ttu-id="24c1d-244">參數</span><span class="sxs-lookup"><span data-stu-id="24c1d-244">Parameter</span></span> | <span data-ttu-id="24c1d-245">說明</span><span class="sxs-lookup"><span data-stu-id="24c1d-245">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="24c1d-246">錯誤</span><span class="sxs-lookup"><span data-stu-id="24c1d-246">error</span></span> |<span data-ttu-id="24c1d-247">用以分類發生的錯誤類型與回應錯誤的錯誤碼字串。</span><span class="sxs-lookup"><span data-stu-id="24c1d-247">An error code string that can be used to classify types of errors that occur, and can be used to react to errors.</span></span> |
| <span data-ttu-id="24c1d-248">error_description</span><span class="sxs-lookup"><span data-stu-id="24c1d-248">error_description</span></span> |<span data-ttu-id="24c1d-249">可協助開發人員識別錯誤根本原因的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="24c1d-249">A specific error message that can help a developer identify the root cause of an error.</span></span> |

<span data-ttu-id="24c1d-250">從系統管理員同意端點收到成功回應之後，您的應用程式便已取得它所要求的權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-250">After you've received a successful response from the admin consent endpoint, your app has gained the permissions it requested.</span></span> <span data-ttu-id="24c1d-251">接著，您可以針對您想要的資源要求權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-251">Next, you can request a token for the resource you want.</span></span>

## <a name="using-permissions"></a><span data-ttu-id="24c1d-252">使用權限</span><span class="sxs-lookup"><span data-stu-id="24c1d-252">Using permissions</span></span>
<span data-ttu-id="24c1d-253">在使用者同意您的應用程式的權限之後，您的應用程式即可取得存取權杖，而這些權杖代表您的應用程式存取資源的權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-253">After the user consents to permissions for your app, your app can acquire access tokens that represent your app's permission to access a resource in some capacity.</span></span> <span data-ttu-id="24c1d-254">一個存取權杖只能用於一個單一資源，但存取權杖內部所編碼的是您應用程式針對該資源已獲得的每項權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-254">An access token can be used only for a single resource, but encoded inside the access token is every permission that your app has been granted for that resource.</span></span> <span data-ttu-id="24c1d-255">若要取得存取權杖，您的應用程式可以對 v2.0 權杖端點提出要求，像這樣：</span><span class="sxs-lookup"><span data-stu-id="24c1d-255">To acquire an access token, your app can make a request to the v2.0 token endpoint, like this:</span></span>

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

<span data-ttu-id="24c1d-256">您可以在對資源提出的 HTTP 要求中使用產生的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="24c1d-256">You can use the resulting access token in HTTP requests to the resource.</span></span> <span data-ttu-id="24c1d-257">它會可靠地向資源指出您的應用程式具有可執行特定工作的適當權限。</span><span class="sxs-lookup"><span data-stu-id="24c1d-257">It reliably indicates to the resource that your app has the proper permission to perform a specific task.</span></span>  

<span data-ttu-id="24c1d-258">如需有關 OAuth 2.0 通訊協定及如何取得存取權杖的詳細資訊，請參閱 [v2.0 端點通訊協定參考](active-directory-v2-protocols.md)。</span><span class="sxs-lookup"><span data-stu-id="24c1d-258">For more information about the OAuth 2.0 protocol and how to get access tokens, see the [v2.0 endpoint protocol reference](active-directory-v2-protocols.md).</span></span>
