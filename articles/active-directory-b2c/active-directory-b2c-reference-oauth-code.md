---
title: "授權碼流程 - Azure AD B2C | Microsoft Docs"
description: "了解如何使用 Azure AD B2C 和 OpenID Connect 的驗證通訊協定來建置 web 應用程式。"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: c371aaab-813a-4317-97df-b62e2f53d865
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: dfc4f2e84704307ccbea6141c0dbc8d089733b22
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-oauth-20-authorization-code-flow"></a><span data-ttu-id="c0be8-103">Azure Active Directory B2C：OAuth 2.0 授權碼流程</span><span class="sxs-lookup"><span data-stu-id="c0be8-103">Azure Active Directory B2C: OAuth 2.0 authorization code flow</span></span>
<span data-ttu-id="c0be8-104">在安裝於裝置上的應用程式中，您可以使用 OAuth 2.0 授權碼授與來存取受保護的資源，例如 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0be8-104">You can use the OAuth 2.0 authorization code grant in apps installed on a device to gain access to protected resources, such as web APIs.</span></span> <span data-ttu-id="c0be8-105">您可以使用 Azure Active Directory B2C (Azure AD B2C) 的 OAuth 2.0 實作，將註冊、登入及其他身分識別管理工作新增至行動及桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0be8-105">By using the Azure Active Directory B2C (Azure AD B2C) implementation of OAuth 2.0, you can add sign-up, sign-in, and other identity management tasks to your mobile and desktop apps.</span></span> <span data-ttu-id="c0be8-106">這篇文章是與語言無關。</span><span class="sxs-lookup"><span data-stu-id="c0be8-106">This article is language-independent.</span></span> <span data-ttu-id="c0be8-107">在本文中，我們將說明如何傳送及接收 HTTP 訊息，但不使用任何開放原始碼程式庫。</span><span class="sxs-lookup"><span data-stu-id="c0be8-107">In the article, we describe how to send and receive HTTP messages without using any open-source libraries.</span></span>

<!-- TODO: Need link to libraries -->

<span data-ttu-id="c0be8-108">如需 OAuth 2.0 授權碼流程的說明，請參閱 [OAuth 2.0 規格的 4.1 節](http://tools.ietf.org/html/rfc6749)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-108">The OAuth 2.0 authorization code flow is described in [section 4.1 of the OAuth 2.0 specification](http://tools.ietf.org/html/rfc6749).</span></span> <span data-ttu-id="c0be8-109">在大多數應用程式類型中 (包括 [Web 應用程式](active-directory-b2c-apps.md#web-apps)和[原生安裝的應用程式](active-directory-b2c-apps.md#mobile-and-native-apps))，您可以利用它來執行驗證及授權作業。</span><span class="sxs-lookup"><span data-stu-id="c0be8-109">You can use it for authentication and authorization in most app types, including [web apps](active-directory-b2c-apps.md#web-apps) and [natively installed apps](active-directory-b2c-apps.md#mobile-and-native-apps).</span></span> <span data-ttu-id="c0be8-110">您可以使用 OAuth 2.0 授權碼流程，安全地為您的應用程式取得「存取權杖」，而這些權杖可用於存取[授權伺服器](active-directory-b2c-reference-protocols.md#the-basics)所保護的資源。</span><span class="sxs-lookup"><span data-stu-id="c0be8-110">You can use the OAuth 2.0 authorization code flow to securely acquire *access tokens* for your apps, which can be used to access resources that are secured by an [authorization server](active-directory-b2c-reference-protocols.md#the-basics).</span></span>

<span data-ttu-id="c0be8-111">本文著重在**公開用戶端** OAuth 2.0 授權碼流程。</span><span class="sxs-lookup"><span data-stu-id="c0be8-111">This article focuses on the **public clients** OAuth 2.0 authorization code flow.</span></span> <span data-ttu-id="c0be8-112">公開用戶端是指不可信任會安全地維護密碼完整性的任何用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0be8-112">A public client is any client application that cannot be trusted to securely maintain the integrity of a secret password.</span></span> <span data-ttu-id="c0be8-113">這包括行動應用程式、桌面應用程式，以及基本上任何在裝置上執行且需要取得存取權杖的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0be8-113">This includes mobile apps, desktop apps, and essentially any application that runs on a device and needs to get access tokens.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0be8-114">若要使用 Azure AD B2C 將身分識別管理新增至 Web 應用程式，請使用 [OpenID Connect](active-directory-b2c-reference-oidc.md)，而不是 OAuth 2.0。</span><span class="sxs-lookup"><span data-stu-id="c0be8-114">To add identity management to a web app by using Azure AD B2C, use [OpenID Connect](active-directory-b2c-reference-oidc.md) instead of OAuth 2.0.</span></span>

<span data-ttu-id="c0be8-115">Azure AD B2C 擴充標準的 OAuth 2.0 流程，功能更強大，而不僅止於簡單的驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="c0be8-115">Azure AD B2C extends the standard OAuth 2.0 flows to do more than simple authentication and authorization.</span></span> <span data-ttu-id="c0be8-116">它引進[原則參數](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-116">It introduces the [policy parameter](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="c0be8-117">透過內建原則，您可以利用 OAuth 2.0 將使用者體驗新增至應用程式，例如註冊、登入和設定檔管理。</span><span class="sxs-lookup"><span data-stu-id="c0be8-117">With built-in policies, you can use OAuth 2.0 to add user experiences to your app, such as sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="c0be8-118">在本文中，我們將示範如何利用 OAuth 2.0 和原則，在您的原生應用程式中實作上述每一種體驗。</span><span class="sxs-lookup"><span data-stu-id="c0be8-118">In this article, we show you how to use OAuth 2.0 and policies to implement each of these experiences in your native applications.</span></span> <span data-ttu-id="c0be8-119">我們也會示範如何取得用來存取 Web API 的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-119">We also show you how to get access tokens for accessing web APIs.</span></span>

<span data-ttu-id="c0be8-120">在本文的範例 HTTP 要求中，我們會使用範例 Azure AD B2C 目錄 **fabrikamb2c.onmicrosoft.com**。此外，也會使用我們的範例應用程式和原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-120">In the example HTTP requests in this article, we use our sample Azure AD B2C directory, **fabrikamb2c.onmicrosoft.com**. We also use our sample application and policies.</span></span> <span data-ttu-id="c0be8-121">您可以使用這些值來自行試驗要求，也可以將它們換成您自己的值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-121">You can try the requests yourself by using these values, or you can replace them with your own values.</span></span>
<span data-ttu-id="c0be8-122">了解如何[取得您自己的 Azure AD B2C 目錄、應用程式和原則](#use-your-own-azure-ad-b2c-directory)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-122">Learn how to [get your own Azure AD B2C directory, application, and policies](#use-your-own-azure-ad-b2c-directory).</span></span>

## <a name="1-get-an-authorization-code"></a><span data-ttu-id="c0be8-123">1.取得授權碼</span><span class="sxs-lookup"><span data-stu-id="c0be8-123">1. Get an authorization code</span></span>
<span data-ttu-id="c0be8-124">授權碼流程始於用戶端將使用者導向 `/authorize` 端點。</span><span class="sxs-lookup"><span data-stu-id="c0be8-124">The authorization code flow begins with the client directing the user to the `/authorize` endpoint.</span></span> <span data-ttu-id="c0be8-125">這是使用者在流程中會採取動作的互動部分。</span><span class="sxs-lookup"><span data-stu-id="c0be8-125">This is the interactive part of the flow, where the user takes action.</span></span> <span data-ttu-id="c0be8-126">在此要求中，用戶端會在 `scope` 參數中指出必須向使用者索取的權限。</span><span class="sxs-lookup"><span data-stu-id="c0be8-126">In this request, the client indicates in the `scope` parameter the permissions that it needs to acquire from the user.</span></span> <span data-ttu-id="c0be8-127">在 `p` 參數中，它會指出要執行的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-127">In the `p` parameter, it indicates the policy to execute.</span></span> <span data-ttu-id="c0be8-128">以下三個範例 (插入換行以提高可讀性) 各使用不同的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-128">The following three examples (with line breaks for readability) each use a different policy.</span></span>

### <a name="use-a-sign-in-policy"></a><span data-ttu-id="c0be8-129">使用登入原則</span><span class="sxs-lookup"><span data-stu-id="c0be8-129">Use a sign-in policy</span></span>
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a><span data-ttu-id="c0be8-130">使用註冊原則</span><span class="sxs-lookup"><span data-stu-id="c0be8-130">Use a sign-up policy</span></span>
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a><span data-ttu-id="c0be8-131">使用編輯設定檔原則</span><span class="sxs-lookup"><span data-stu-id="c0be8-131">Use an edit-profile policy</span></span>
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code
&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob
&response_mode=query
&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&p=b2c_1_edit_profile
```

| <span data-ttu-id="c0be8-132">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-132">Parameter</span></span> | <span data-ttu-id="c0be8-133">必要？</span><span class="sxs-lookup"><span data-stu-id="c0be8-133">Required?</span></span> | <span data-ttu-id="c0be8-134">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0be8-135">client_id</span><span class="sxs-lookup"><span data-stu-id="c0be8-135">client_id</span></span> |<span data-ttu-id="c0be8-136">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-136">Required</span></span> |<span data-ttu-id="c0be8-137">在 [Azure 入口網站](https://portal.azure.com)中指派給應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-137">The application ID assigned to your app in the [Azure portal](https://portal.azure.com).</span></span> |
| <span data-ttu-id="c0be8-138">response_type</span><span class="sxs-lookup"><span data-stu-id="c0be8-138">response_type</span></span> |<span data-ttu-id="c0be8-139">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-139">Required</span></span> |<span data-ttu-id="c0be8-140">回應類型，必須針對授權碼流程來加入 `code`。</span><span class="sxs-lookup"><span data-stu-id="c0be8-140">The response type, which must include `code` for the authorization code flow.</span></span> |
| <span data-ttu-id="c0be8-141">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="c0be8-141">redirect_uri</span></span> |<span data-ttu-id="c0be8-142">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-142">Required</span></span> |<span data-ttu-id="c0be8-143">應用程式的重新導向 URI，您的應用程式會在此處傳送及接收驗證回應。</span><span class="sxs-lookup"><span data-stu-id="c0be8-143">The redirect URI of your app, where authentication responses are sent and received by your app.</span></span> <span data-ttu-id="c0be8-144">除了必須是 URL 編碼，它必須與您在入口網站中註冊的其中一個重新導向 URI 完全相符。</span><span class="sxs-lookup"><span data-stu-id="c0be8-144">It must exactly match one of the redirect URIs that you registered in the portal, except that it must be URL-encoded.</span></span> |
| <span data-ttu-id="c0be8-145">scope</span><span class="sxs-lookup"><span data-stu-id="c0be8-145">scope</span></span> |<span data-ttu-id="c0be8-146">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-146">Required</span></span> |<span data-ttu-id="c0be8-147">範圍的空格分隔清單。</span><span class="sxs-lookup"><span data-stu-id="c0be8-147">A space-separated list of scopes.</span></span> <span data-ttu-id="c0be8-148">單一範圍值向 Azure Active Directory (Azure AD) 指出正在要求的兩個權限。</span><span class="sxs-lookup"><span data-stu-id="c0be8-148">A single scope value indicates to Azure Active Directory (Azure AD) both of the permissions that are being requested.</span></span> <span data-ttu-id="c0be8-149">使用用戶端識別碼作為範圍時，表示您的應用程式需要可針對您自己的服務或 Web API 使用的存取權杖 (以相同的用戶端識別碼表示)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-149">Using the client ID as the scope indicates that your app needs an access token that can be used against your own service or web API, represented by the same client ID.</span></span>  <span data-ttu-id="c0be8-150">`offline_access` 範圍表示您的應用程式需要重新整理權杖，才能長久存取資源。</span><span class="sxs-lookup"><span data-stu-id="c0be8-150">The `offline_access` scope indicates that your app needs a refresh token for long-lived access to resources.</span></span> <span data-ttu-id="c0be8-151">您也可以使用 `openid` 範圍從 Azure AD B2C 要求識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-151">You also can use the `openid` scope to request an ID token from Azure AD B2C.</span></span> |
| <span data-ttu-id="c0be8-152">response_mode</span><span class="sxs-lookup"><span data-stu-id="c0be8-152">response_mode</span></span> |<span data-ttu-id="c0be8-153">建議</span><span class="sxs-lookup"><span data-stu-id="c0be8-153">Recommended</span></span> |<span data-ttu-id="c0be8-154">用來將產生的授權碼傳回至應用程式的方法。</span><span class="sxs-lookup"><span data-stu-id="c0be8-154">The method that you use to send the resulting authorization code back to your app.</span></span> <span data-ttu-id="c0be8-155">可以是 `query`、`form_post` 或 `fragment`。</span><span class="sxs-lookup"><span data-stu-id="c0be8-155">It can be `query`, `form_post`, or `fragment`.</span></span> |
| <span data-ttu-id="c0be8-156">state</span><span class="sxs-lookup"><span data-stu-id="c0be8-156">state</span></span> |<span data-ttu-id="c0be8-157">建議</span><span class="sxs-lookup"><span data-stu-id="c0be8-157">Recommended</span></span> |<span data-ttu-id="c0be8-158">會隨權杖回應傳回之要求中所包含的值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-158">A value included in the request that is returned in the token response.</span></span> <span data-ttu-id="c0be8-159">它可以是您想要使用之任何內容的字串。</span><span class="sxs-lookup"><span data-stu-id="c0be8-159">It can be a string of any content that you want to use.</span></span> <span data-ttu-id="c0be8-160">通常會使用隨機產生的唯一值，以防止跨網站偽造要求攻擊。</span><span class="sxs-lookup"><span data-stu-id="c0be8-160">Usually, a randomly generated unique value is  used, to prevent cross-site request forgery attacks.</span></span> <span data-ttu-id="c0be8-161">在驗證要求出現之前，也會使用此狀態將應用程式中使用者狀態的相關資訊編碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-161">The state also is used to encode information about the user's state in the app before the authentication request occurred.</span></span> <span data-ttu-id="c0be8-162">例如，使用者所在的頁面，或正在執行的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-162">For example, the page the user was on, or the policy that was being executed.</span></span> |
| <span data-ttu-id="c0be8-163">p</span><span class="sxs-lookup"><span data-stu-id="c0be8-163">p</span></span> |<span data-ttu-id="c0be8-164">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-164">Required</span></span> |<span data-ttu-id="c0be8-165">執行的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-165">The policy that is executed.</span></span> <span data-ttu-id="c0be8-166">這是在您的 Azure AD B2C 目錄中建立的原則名稱。</span><span class="sxs-lookup"><span data-stu-id="c0be8-166">It's the name of a policy that is created in your Azure AD B2C directory.</span></span> <span data-ttu-id="c0be8-167">原則名稱值的開頭應該為**b2c\_1\_**。</span><span class="sxs-lookup"><span data-stu-id="c0be8-167">The policy name value should begin with **b2c\_1\_**.</span></span> <span data-ttu-id="c0be8-168">若要深入了解原則，請參閱 [Azure AD B2C 內建原則](active-directory-b2c-reference-policies.md)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-168">To learn more about policies, see [Azure AD B2C built-in policies](active-directory-b2c-reference-policies.md).</span></span> |
| <span data-ttu-id="c0be8-169">prompt</span><span class="sxs-lookup"><span data-stu-id="c0be8-169">prompt</span></span> |<span data-ttu-id="c0be8-170">選用</span><span class="sxs-lookup"><span data-stu-id="c0be8-170">Optional</span></span> |<span data-ttu-id="c0be8-171">需要的使用者互動類型。</span><span class="sxs-lookup"><span data-stu-id="c0be8-171">The type of user interaction that is required.</span></span> <span data-ttu-id="c0be8-172">目前，唯一有效的值是 `login`，可強制使用者針對該要求輸入其認證。</span><span class="sxs-lookup"><span data-stu-id="c0be8-172">Currently, the only valid value is `login`, which forces the user to enter their credentials on that request.</span></span> <span data-ttu-id="c0be8-173">單一登入將沒有作用。</span><span class="sxs-lookup"><span data-stu-id="c0be8-173">Single sign-on will not take effect.</span></span> |

<span data-ttu-id="c0be8-174">此時會要求使用者完成原則的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c0be8-174">At this point, the user is asked to complete the policy's workflow.</span></span> <span data-ttu-id="c0be8-175">這可能會牽涉到讓使用者輸入自己的使用者名稱及密碼、以社交身分識別登入、註冊目錄，或是其他任何數目的步驟。</span><span class="sxs-lookup"><span data-stu-id="c0be8-175">This might involve the user entering their username and password, signing in with a social identity, signing up for the directory, or any other number of steps.</span></span> <span data-ttu-id="c0be8-176">使用者動作取決於原則的定義方式。</span><span class="sxs-lookup"><span data-stu-id="c0be8-176">User actions depend on how the policy is defined.</span></span>

<span data-ttu-id="c0be8-177">當使用者完成原則之後，Azure AD 會透過您用於 `redirect_uri` 的值，將回應傳回給您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c0be8-177">After the user completes the policy, Azure AD returns a response to your app at the value you used for `redirect_uri`.</span></span> <span data-ttu-id="c0be8-178">它會使用 `response_mode` 參數中指定的方法。</span><span class="sxs-lookup"><span data-stu-id="c0be8-178">It uses the method specified in the `response_mode` parameter.</span></span> <span data-ttu-id="c0be8-179">對於每個使用者動作情節來說，回應完全相同，與已執行的原則無關。</span><span class="sxs-lookup"><span data-stu-id="c0be8-179">The response is exactly the same for each of the user action scenarios, independent of the policy that was executed.</span></span>

<span data-ttu-id="c0be8-180">使用 `response_mode=query` 的成功回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0be8-180">A successful response that uses `response_mode=query` looks like this:</span></span>

```
GET urn:ietf:wg:oauth:2.0:oob?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...        // the authorization_code, truncated
&state=arbitrary_data_you_can_receive_in_the_response                // the value provided in the request
```

| <span data-ttu-id="c0be8-181">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-181">Parameter</span></span> | <span data-ttu-id="c0be8-182">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-182">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0be8-183">code</span><span class="sxs-lookup"><span data-stu-id="c0be8-183">code</span></span> |<span data-ttu-id="c0be8-184">應用程式所要求的授權碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-184">The authorization code that the app requested.</span></span> <span data-ttu-id="c0be8-185">應用程式可以使用授權碼來要求目標資源的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-185">The app can use the authorization code to request an access token for a target resource.</span></span> <span data-ttu-id="c0be8-186">授權碼的存留期很短。</span><span class="sxs-lookup"><span data-stu-id="c0be8-186">Authorization codes are very short-lived.</span></span> <span data-ttu-id="c0be8-187">通常會在大約 10 分鐘後過期。</span><span class="sxs-lookup"><span data-stu-id="c0be8-187">Typically, they expire after about 10 minutes.</span></span> |
| <span data-ttu-id="c0be8-188">state</span><span class="sxs-lookup"><span data-stu-id="c0be8-188">state</span></span> |<span data-ttu-id="c0be8-189">如需完整說明，請參閱上一節的表格。</span><span class="sxs-lookup"><span data-stu-id="c0be8-189">See the full description in the table in the preceding section.</span></span> <span data-ttu-id="c0be8-190">如果要求中包含 `state` 參數，回應中就應該出現相同的值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-190">If a `state` parameter is included in the request, the same value should appear in the response.</span></span> <span data-ttu-id="c0be8-191">應用程式應該驗證要求和回應中的 `state` 值完全相同。</span><span class="sxs-lookup"><span data-stu-id="c0be8-191">The app should verify that the `state` values in the request and response are identical.</span></span> |

<span data-ttu-id="c0be8-192">錯誤回應也能傳送到重新導向 URI，以便讓應用程式能夠適當地處理它們：</span><span class="sxs-lookup"><span data-stu-id="c0be8-192">Error responses also can be sent to the redirect URI so that the app can handle them appropriately:</span></span>

```
GET urn:ietf:wg:oauth:2.0:oob?
error=access_denied
&error_description=The+user+has+cancelled+entering+self-asserted+information
&state=arbitrary_data_you_can_receive_in_the_response
```

| <span data-ttu-id="c0be8-193">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-193">Parameter</span></span> | <span data-ttu-id="c0be8-194">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-194">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0be8-195">錯誤</span><span class="sxs-lookup"><span data-stu-id="c0be8-195">error</span></span> |<span data-ttu-id="c0be8-196">可用於將發生的錯誤類型分類的錯誤碼字串。</span><span class="sxs-lookup"><span data-stu-id="c0be8-196">An error code string that you can use to classify the types of errors that occur.</span></span> <span data-ttu-id="c0be8-197">您也可以使用此字串對錯誤做出反應。</span><span class="sxs-lookup"><span data-stu-id="c0be8-197">You also can use the string to react to errors.</span></span> |
| <span data-ttu-id="c0be8-198">error_description</span><span class="sxs-lookup"><span data-stu-id="c0be8-198">error_description</span></span> |<span data-ttu-id="c0be8-199">可協助您識別驗證錯誤根本原因的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c0be8-199">A specific error message that can help you identify the root cause of an authentication error.</span></span> |
| <span data-ttu-id="c0be8-200">state</span><span class="sxs-lookup"><span data-stu-id="c0be8-200">state</span></span> |<span data-ttu-id="c0be8-201">如需完整說明，請參閱前一個表格。</span><span class="sxs-lookup"><span data-stu-id="c0be8-201">See the full description in the preceding table.</span></span> <span data-ttu-id="c0be8-202">如果要求中包含 `state` 參數，回應中就應該出現相同的值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-202">If a `state` parameter is included in the request, the same value should appear in the response.</span></span> <span data-ttu-id="c0be8-203">應用程式應該驗證要求和回應中的 `state` 值完全相同。</span><span class="sxs-lookup"><span data-stu-id="c0be8-203">The app should verify that the `state` values in the request and response are identical.</span></span> |

## <a name="2-get-a-token"></a><span data-ttu-id="c0be8-204">2.取得權杖</span><span class="sxs-lookup"><span data-stu-id="c0be8-204">2. Get a token</span></span>
<span data-ttu-id="c0be8-205">既然已取得授權碼，您可以將 POST 要求傳送至 `/token` 端點，針對所需的資源來兌換權杖的 `code`。</span><span class="sxs-lookup"><span data-stu-id="c0be8-205">Now that you've acquired an authorization code, you can redeem the `code` for a token to the intended resource by sending a POST request to the `/token` endpoint.</span></span> <span data-ttu-id="c0be8-206">在 Azure AD B2C 中，您唯一可以要求權杖的資源，就是應用程式本身的後端 Web API。</span><span class="sxs-lookup"><span data-stu-id="c0be8-206">In Azure AD B2C, the only resource that you can request a token for is your app's own back-end web API.</span></span> <span data-ttu-id="c0be8-207">為您自己要求權杖時，依慣例會使用應用程式的用戶端識別碼作為範圍：</span><span class="sxs-lookup"><span data-stu-id="c0be8-207">The convention that's used for requesting a token to yourself is to use your app's client ID as the scope:</span></span>

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob

```

| <span data-ttu-id="c0be8-208">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-208">Parameter</span></span> | <span data-ttu-id="c0be8-209">必要？</span><span class="sxs-lookup"><span data-stu-id="c0be8-209">Required?</span></span> | <span data-ttu-id="c0be8-210">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-210">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0be8-211">p</span><span class="sxs-lookup"><span data-stu-id="c0be8-211">p</span></span> |<span data-ttu-id="c0be8-212">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-212">Required</span></span> |<span data-ttu-id="c0be8-213">用來取得授權碼的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-213">The policy that was used to acquire the authorization code.</span></span> <span data-ttu-id="c0be8-214">您無法在此要求中使用不同的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-214">You cannot use a different policy in this request.</span></span> <span data-ttu-id="c0be8-215">請注意，您要把這個參數新增到「查詢字串」 ，而不是 POST 主體中。</span><span class="sxs-lookup"><span data-stu-id="c0be8-215">Note that you add this parameter to the *query string*, not in the POST body.</span></span> |
| <span data-ttu-id="c0be8-216">client_id</span><span class="sxs-lookup"><span data-stu-id="c0be8-216">client_id</span></span> |<span data-ttu-id="c0be8-217">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-217">Required</span></span> |<span data-ttu-id="c0be8-218">在 [Azure 入口網站](https://portal.azure.com)中指派給應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-218">The application ID assigned to your app in the [Azure portal](https://portal.azure.com).</span></span> |
| <span data-ttu-id="c0be8-219">grant_type</span><span class="sxs-lookup"><span data-stu-id="c0be8-219">grant_type</span></span> |<span data-ttu-id="c0be8-220">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-220">Required</span></span> |<span data-ttu-id="c0be8-221">授與類型。</span><span class="sxs-lookup"><span data-stu-id="c0be8-221">The type of grant.</span></span> <span data-ttu-id="c0be8-222">在授權碼流程中，授與類型必須的 `authorization_code`。</span><span class="sxs-lookup"><span data-stu-id="c0be8-222">For the authorization code flow, the grant type must be `authorization_code`.</span></span> |
| <span data-ttu-id="c0be8-223">scope</span><span class="sxs-lookup"><span data-stu-id="c0be8-223">scope</span></span> |<span data-ttu-id="c0be8-224">建議</span><span class="sxs-lookup"><span data-stu-id="c0be8-224">Recommended</span></span> |<span data-ttu-id="c0be8-225">範圍的空格分隔清單。</span><span class="sxs-lookup"><span data-stu-id="c0be8-225">A space-separated list of scopes.</span></span> <span data-ttu-id="c0be8-226">單一範圍值，向 Azure AD 指出受到要求的兩個權限。</span><span class="sxs-lookup"><span data-stu-id="c0be8-226">A single scope value indicates to Azure AD both of the permissions that are being requested.</span></span> <span data-ttu-id="c0be8-227">使用用戶端識別碼作為範圍時，表示您的應用程式需要可針對您自己的服務或 Web API 使用的存取權杖 (以相同的用戶端識別碼表示)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-227">Using the client ID as the scope indicates that your app needs an access token that can be used against your own service or web API, represented by the same client ID.</span></span>  <span data-ttu-id="c0be8-228">`offline_access` 範圍表示您的應用程式需要重新整理權杖，才能長久存取資源。</span><span class="sxs-lookup"><span data-stu-id="c0be8-228">The `offline_access` scope indicates that your app needs a refresh token for long-lived access to resources.</span></span>  <span data-ttu-id="c0be8-229">您也可以使用 `openid` 範圍從 Azure AD B2C 要求識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-229">You also can use the `openid` scope to request an ID token from Azure AD B2C.</span></span> |
| <span data-ttu-id="c0be8-230">code</span><span class="sxs-lookup"><span data-stu-id="c0be8-230">code</span></span> |<span data-ttu-id="c0be8-231">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-231">Required</span></span> |<span data-ttu-id="c0be8-232">您在流程的第一個階段中取得的授權碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-232">The authorization code that you acquired in the first leg of the flow.</span></span> |
| <span data-ttu-id="c0be8-233">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="c0be8-233">redirect_uri</span></span> |<span data-ttu-id="c0be8-234">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-234">Required</span></span> |<span data-ttu-id="c0be8-235">應用程式的重新導向 URI，您已在此處收到授權碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-235">The redirect URI of the application where you received the authorization code.</span></span> |

<span data-ttu-id="c0be8-236">成功的權杖回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0be8-236">A successful token response looks like this:</span></span>

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| <span data-ttu-id="c0be8-237">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-237">Parameter</span></span> | <span data-ttu-id="c0be8-238">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-238">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0be8-239">not_before</span><span class="sxs-lookup"><span data-stu-id="c0be8-239">not_before</span></span> |<span data-ttu-id="c0be8-240">權杖生效的時間 (以新紀元 (Epoch) 時間表示)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-240">The time at which the token is considered valid, in epoch time.</span></span> |
| <span data-ttu-id="c0be8-241">token_type</span><span class="sxs-lookup"><span data-stu-id="c0be8-241">token_type</span></span> |<span data-ttu-id="c0be8-242">權杖類型值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-242">The token type value.</span></span> <span data-ttu-id="c0be8-243">Azure AD 唯一支援的類型是 Bearer。</span><span class="sxs-lookup"><span data-stu-id="c0be8-243">The only type that Azure AD supports is Bearer.</span></span> |
| <span data-ttu-id="c0be8-244">access_token</span><span class="sxs-lookup"><span data-stu-id="c0be8-244">access_token</span></span> |<span data-ttu-id="c0be8-245">您所要求的已簽署 JSON Web 權杖 (JWT)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-245">The signed JSON Web Token (JWT) that you requested.</span></span> |
| <span data-ttu-id="c0be8-246">scope</span><span class="sxs-lookup"><span data-stu-id="c0be8-246">scope</span></span> |<span data-ttu-id="c0be8-247">權杖有效的範圍。</span><span class="sxs-lookup"><span data-stu-id="c0be8-247">The scopes that the token is valid for.</span></span> <span data-ttu-id="c0be8-248">您也可以使用範圍來快取權杖，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="c0be8-248">You also can use scopes to cache tokens for later use.</span></span> |
| <span data-ttu-id="c0be8-249">expires_in</span><span class="sxs-lookup"><span data-stu-id="c0be8-249">expires_in</span></span> |<span data-ttu-id="c0be8-250">權杖的有效時間長度 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-250">The length of time that the token is valid (in seconds).</span></span> |
| <span data-ttu-id="c0be8-251">refresh_token</span><span class="sxs-lookup"><span data-stu-id="c0be8-251">refresh_token</span></span> |<span data-ttu-id="c0be8-252">OAuth 2.0 重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-252">An OAuth 2.0 refresh token.</span></span> <span data-ttu-id="c0be8-253">應用程式在目前的權杖過期之後，可以使用這個權杖來取得其他權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-253">The app can use this token to acquire additional tokens after the current token expires.</span></span> <span data-ttu-id="c0be8-254">重新整理權杖是長期權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-254">Refresh tokens are long-lived.</span></span> <span data-ttu-id="c0be8-255">您可以使用它們來長時間持續存取資源。</span><span class="sxs-lookup"><span data-stu-id="c0be8-255">You can use them to retain access to resources for extended periods of time.</span></span> <span data-ttu-id="c0be8-256">如需詳細資訊，請參閱 [Azure AD B2C 權杖參考](active-directory-b2c-reference-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-256">For more information, see the [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span> |

<span data-ttu-id="c0be8-257">錯誤回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0be8-257">Error responses look like this:</span></span>

```
{
    "error": "access_denied",
    "error_description": "The user revoked access to the app.",
}
```

| <span data-ttu-id="c0be8-258">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-258">Parameter</span></span> | <span data-ttu-id="c0be8-259">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-259">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0be8-260">錯誤</span><span class="sxs-lookup"><span data-stu-id="c0be8-260">error</span></span> |<span data-ttu-id="c0be8-261">可用於將發生的錯誤類型分類的錯誤碼字串。</span><span class="sxs-lookup"><span data-stu-id="c0be8-261">An error code string that you can use to classify the types of errors that occur.</span></span> <span data-ttu-id="c0be8-262">您也可以使用此字串對錯誤做出反應。</span><span class="sxs-lookup"><span data-stu-id="c0be8-262">You also can use the string to react to errors.</span></span> |
| <span data-ttu-id="c0be8-263">error_description</span><span class="sxs-lookup"><span data-stu-id="c0be8-263">error_description</span></span> |<span data-ttu-id="c0be8-264">可協助您識別驗證錯誤根本原因的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c0be8-264">A specific error message that can help you identify the root cause of an authentication error.</span></span> |

## <a name="3-use-the-token"></a><span data-ttu-id="c0be8-265">3.使用權杖</span><span class="sxs-lookup"><span data-stu-id="c0be8-265">3. Use the token</span></span>
<span data-ttu-id="c0be8-266">既然已成功取得存取權杖，在對後端 Web API 發出的要求中，您可以將權杖加入 `Authorization` 標頭中，即可使用權杖：</span><span class="sxs-lookup"><span data-stu-id="c0be8-266">Now that you've successfully acquired an access token, you can use the token in requests to your back-end web APIs by including it in the `Authorization` header:</span></span>

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="4-refresh-the-token"></a><span data-ttu-id="c0be8-267">4.重新整理權杖</span><span class="sxs-lookup"><span data-stu-id="c0be8-267">4. Refresh the token</span></span>
<span data-ttu-id="c0be8-268">存取權杖和識別碼權杖的存留期短暫。</span><span class="sxs-lookup"><span data-stu-id="c0be8-268">Access tokens and ID tokens are short-lived.</span></span> <span data-ttu-id="c0be8-269">權杖過期之後，您必須重新整理權杖，才能繼續存取資源。</span><span class="sxs-lookup"><span data-stu-id="c0be8-269">After they expire, you must refresh them to continue to access resources.</span></span> <span data-ttu-id="c0be8-270">若要這樣做，請向 `/token` 端點提交另一個 POST 要求。</span><span class="sxs-lookup"><span data-stu-id="c0be8-270">To do this, submit another POST request to the `/token` endpoint.</span></span> <span data-ttu-id="c0be8-271">但這次要提供 `refresh_token`，而不是 `code`：</span><span class="sxs-lookup"><span data-stu-id="c0be8-271">This time, provide the `refresh_token` instead of the `code`:</span></span>

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob
```

| <span data-ttu-id="c0be8-272">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-272">Parameter</span></span> | <span data-ttu-id="c0be8-273">必要？</span><span class="sxs-lookup"><span data-stu-id="c0be8-273">Required?</span></span> | <span data-ttu-id="c0be8-274">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-274">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c0be8-275">p</span><span class="sxs-lookup"><span data-stu-id="c0be8-275">p</span></span> |<span data-ttu-id="c0be8-276">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-276">Required</span></span> |<span data-ttu-id="c0be8-277">用來取得原始重新整理權杖的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-277">The policy that was used to acquire the original refresh token.</span></span> <span data-ttu-id="c0be8-278">您無法在此要求中使用不同的原則。</span><span class="sxs-lookup"><span data-stu-id="c0be8-278">You cannot use a different policy in this request.</span></span> <span data-ttu-id="c0be8-279">請注意，您要把這個參數新增到「查詢字串」 ，而不是 POST 主體中。</span><span class="sxs-lookup"><span data-stu-id="c0be8-279">Note that you add this parameter to the *query string*, not in the POST body.</span></span> |
| <span data-ttu-id="c0be8-280">client_id</span><span class="sxs-lookup"><span data-stu-id="c0be8-280">client_id</span></span> |<span data-ttu-id="c0be8-281">建議</span><span class="sxs-lookup"><span data-stu-id="c0be8-281">Recommended</span></span> |<span data-ttu-id="c0be8-282">在 [Azure 入口網站](https://portal.azure.com)中指派給應用程式的應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-282">The application ID assigned to your app in the [Azure portal](https://portal.azure.com).</span></span> |
| <span data-ttu-id="c0be8-283">grant_type</span><span class="sxs-lookup"><span data-stu-id="c0be8-283">grant_type</span></span> |<span data-ttu-id="c0be8-284">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-284">Required</span></span> |<span data-ttu-id="c0be8-285">授與類型。</span><span class="sxs-lookup"><span data-stu-id="c0be8-285">The type of grant.</span></span> <span data-ttu-id="c0be8-286">在授權碼流程的這個階段中，授與類型必須是 `refresh_token`。</span><span class="sxs-lookup"><span data-stu-id="c0be8-286">For this leg of the authorization code flow, the grant type must be `refresh_token`.</span></span> |
| <span data-ttu-id="c0be8-287">scope</span><span class="sxs-lookup"><span data-stu-id="c0be8-287">scope</span></span> |<span data-ttu-id="c0be8-288">建議</span><span class="sxs-lookup"><span data-stu-id="c0be8-288">Recommended</span></span> |<span data-ttu-id="c0be8-289">範圍的空格分隔清單。</span><span class="sxs-lookup"><span data-stu-id="c0be8-289">A space-separated list of scopes.</span></span> <span data-ttu-id="c0be8-290">單一範圍值，向 Azure AD 指出受到要求的兩個權限。</span><span class="sxs-lookup"><span data-stu-id="c0be8-290">A single scope value indicates to Azure AD both of the permissions that are being requested.</span></span> <span data-ttu-id="c0be8-291">使用用戶端識別碼作為範圍時，表示您的應用程式需要可針對您自己的服務或 Web API 使用的存取權杖 (以相同的用戶端識別碼表示)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-291">Using the client ID as the scope indicates that your app needs an access token that can be used against your own service or web API, represented by the same client ID.</span></span>  <span data-ttu-id="c0be8-292">`offline_access` 範圍表示您的應用程式需要重新整理權杖，才能長久存取資源。</span><span class="sxs-lookup"><span data-stu-id="c0be8-292">The `offline_access` scope indicates that your app will need a refresh token for long-lived access to resources.</span></span>  <span data-ttu-id="c0be8-293">您也可以使用 `openid` 範圍從 Azure AD B2C 要求識別碼權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-293">You also can use the `openid` scope to request an ID token from Azure AD B2C.</span></span> |
| <span data-ttu-id="c0be8-294">redirect_uri</span><span class="sxs-lookup"><span data-stu-id="c0be8-294">redirect_uri</span></span> |<span data-ttu-id="c0be8-295">選用</span><span class="sxs-lookup"><span data-stu-id="c0be8-295">Optional</span></span> |<span data-ttu-id="c0be8-296">應用程式的重新導向 URI，您已在此處收到授權碼。</span><span class="sxs-lookup"><span data-stu-id="c0be8-296">The redirect URI of the application where you received the authorization code.</span></span> |
| <span data-ttu-id="c0be8-297">refresh_token</span><span class="sxs-lookup"><span data-stu-id="c0be8-297">refresh_token</span></span> |<span data-ttu-id="c0be8-298">必要</span><span class="sxs-lookup"><span data-stu-id="c0be8-298">Required</span></span> |<span data-ttu-id="c0be8-299">您在流程的第二個階段中取得的原始重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-299">The original refresh token that you acquired in the second leg of the flow.</span></span> |

<span data-ttu-id="c0be8-300">成功的權杖回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0be8-300">A successful token response looks like this:</span></span>

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| <span data-ttu-id="c0be8-301">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-301">Parameter</span></span> | <span data-ttu-id="c0be8-302">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-302">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0be8-303">not_before</span><span class="sxs-lookup"><span data-stu-id="c0be8-303">not_before</span></span> |<span data-ttu-id="c0be8-304">權杖生效的時間 (以新紀元 (Epoch) 時間表示)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-304">The time at which the token is considered valid, in epoch time.</span></span> |
| <span data-ttu-id="c0be8-305">token_type</span><span class="sxs-lookup"><span data-stu-id="c0be8-305">token_type</span></span> |<span data-ttu-id="c0be8-306">權杖類型值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-306">The token type value.</span></span> <span data-ttu-id="c0be8-307">Azure AD 唯一支援的類型是 Bearer。</span><span class="sxs-lookup"><span data-stu-id="c0be8-307">The only type that Azure AD supports is Bearer.</span></span> |
| <span data-ttu-id="c0be8-308">access_token</span><span class="sxs-lookup"><span data-stu-id="c0be8-308">access_token</span></span> |<span data-ttu-id="c0be8-309">您所要求的已簽署 JWT。</span><span class="sxs-lookup"><span data-stu-id="c0be8-309">The signed JWT that you requested.</span></span> |
| <span data-ttu-id="c0be8-310">scope</span><span class="sxs-lookup"><span data-stu-id="c0be8-310">scope</span></span> |<span data-ttu-id="c0be8-311">權杖有效的範圍。</span><span class="sxs-lookup"><span data-stu-id="c0be8-311">The scopes that the token is valid for.</span></span> <span data-ttu-id="c0be8-312">您也可以使用範圍來快取權杖，以供稍後使用。</span><span class="sxs-lookup"><span data-stu-id="c0be8-312">You also can use the scopes to cache tokens for later use.</span></span> |
| <span data-ttu-id="c0be8-313">expires_in</span><span class="sxs-lookup"><span data-stu-id="c0be8-313">expires_in</span></span> |<span data-ttu-id="c0be8-314">權杖的有效時間長度 (以秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-314">The length of time that the token is valid (in seconds).</span></span> |
| <span data-ttu-id="c0be8-315">refresh_token</span><span class="sxs-lookup"><span data-stu-id="c0be8-315">refresh_token</span></span> |<span data-ttu-id="c0be8-316">OAuth 2.0 重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-316">An OAuth 2.0 refresh token.</span></span> <span data-ttu-id="c0be8-317">應用程式在目前的權杖過期之後，可以使用這個權杖來取得其他權杖。</span><span class="sxs-lookup"><span data-stu-id="c0be8-317">The app can use this token to acquire additional tokens after the current token expires.</span></span> <span data-ttu-id="c0be8-318">重新整理權杖的有效期很長，而且可以用來長期保留資源存取權。</span><span class="sxs-lookup"><span data-stu-id="c0be8-318">Refresh tokens are long-lived, and can be used to retain access to resources for extended periods of time.</span></span> <span data-ttu-id="c0be8-319">如需詳細資訊，請參閱 [Azure AD B2C 權杖參考](active-directory-b2c-reference-tokens.md)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-319">For more information, see the [Azure AD B2C token reference](active-directory-b2c-reference-tokens.md).</span></span> |

<span data-ttu-id="c0be8-320">錯誤回應如下所示：</span><span class="sxs-lookup"><span data-stu-id="c0be8-320">Error responses look like this:</span></span>

```
{
    "error": "access_denied",
    "error_description": "The user revoked access to the app.",
}
```

| <span data-ttu-id="c0be8-321">參數</span><span class="sxs-lookup"><span data-stu-id="c0be8-321">Parameter</span></span> | <span data-ttu-id="c0be8-322">說明</span><span class="sxs-lookup"><span data-stu-id="c0be8-322">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0be8-323">錯誤</span><span class="sxs-lookup"><span data-stu-id="c0be8-323">error</span></span> |<span data-ttu-id="c0be8-324">可用於將發生的錯誤類型分類的錯誤碼字串。</span><span class="sxs-lookup"><span data-stu-id="c0be8-324">An error code string that you can use to classify types of errors that occur.</span></span> <span data-ttu-id="c0be8-325">您也可以使用此字串對錯誤做出反應。</span><span class="sxs-lookup"><span data-stu-id="c0be8-325">You also can use the string to react to errors.</span></span> |
| <span data-ttu-id="c0be8-326">error_description</span><span class="sxs-lookup"><span data-stu-id="c0be8-326">error_description</span></span> |<span data-ttu-id="c0be8-327">可協助您識別驗證錯誤根本原因的特定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="c0be8-327">A specific error message that can help you identify the root cause of an authentication error.</span></span> |

## <a name="use-your-own-azure-ad-b2c-directory"></a><span data-ttu-id="c0be8-328">使用您自己的 Azure AD B2C 目錄</span><span class="sxs-lookup"><span data-stu-id="c0be8-328">Use your own Azure AD B2C directory</span></span>
<span data-ttu-id="c0be8-329">若要自行嘗試這些要求，請完成下列步驟。</span><span class="sxs-lookup"><span data-stu-id="c0be8-329">To try these requests yourself, complete the following steps.</span></span> <span data-ttu-id="c0be8-330">使用您自己的值取代我們在本文中使用的範例值。</span><span class="sxs-lookup"><span data-stu-id="c0be8-330">Replace the example values we used in this article with your own values.</span></span>

1. <span data-ttu-id="c0be8-331">[建立 Azure AD B2C 目錄](active-directory-b2c-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c0be8-331">[Create an Azure AD B2C directory](active-directory-b2c-get-started.md).</span></span> <span data-ttu-id="c0be8-332">在要求中使用您的目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="c0be8-332">Use the name of your directory in the requests.</span></span>
2. <span data-ttu-id="c0be8-333">[建立應用程式](active-directory-b2c-app-registration.md)來取得應用程式識別碼和重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="c0be8-333">[Create an application](active-directory-b2c-app-registration.md) to obtain an application ID and a redirect URI.</span></span> <span data-ttu-id="c0be8-334">在您的應用程式中包含原生用戶端。</span><span class="sxs-lookup"><span data-stu-id="c0be8-334">Include a native client in your app.</span></span>
3. <span data-ttu-id="c0be8-335">[建立您的原則](active-directory-b2c-reference-policies.md) 來取得原則名稱。</span><span class="sxs-lookup"><span data-stu-id="c0be8-335">[Create your policies](active-directory-b2c-reference-policies.md) to obtain your policy names.</span></span>

