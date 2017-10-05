---
title: "如何建置可讓任何 Azure AD 使用者登入的應用程式 | Microsoft Docs"
description: "如何建置可讓使用者從任何 Azure Active Directory 租用戶登入之應用程式 (也稱為多租用戶應用程式) 的逐步解說。"
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: f1c79fa7e3b0e160487b5941741f6a6c677c6b81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-sign-in-any-azure-active-directory-ad-user-using-the-multi-tenant-application-pattern"></a><span data-ttu-id="35324-103">如何使用多租用戶應用程式模式登入任何 Azure Active Directory (AD) 使用者</span><span class="sxs-lookup"><span data-stu-id="35324-103">How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern</span></span>
<span data-ttu-id="35324-104">如果您提供「軟體即服務」應用程式給許多公司，您可以將您的應用程式設定為可接受來自任何 Azure AD 租用戶的登入。</span><span class="sxs-lookup"><span data-stu-id="35324-104">If you offer a Software as a Service application to many organizations, you can configure your application to accept sign-ins from any Azure AD tenant.</span></span>  <span data-ttu-id="35324-105">在 Azure AD 中，這稱為讓您的應用程式成為多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-105">In Azure AD this is called making your application multi-tenant.</span></span>  <span data-ttu-id="35324-106">任何 Azure AD 租用戶中的使用者在同意搭配您的應用程式使用其帳戶之後，便可登入您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-106">Users in any Azure AD tenant will be able to sign in to your application after consenting to use their account with your application.</span></span>  

<span data-ttu-id="35324-107">如果您的現有應用程式有其自己的帳戶系統，或支援從其他雲端提供者執行其他登入方式，則新增從任何租用戶執行 Azure AD 登入很簡單。</span><span class="sxs-lookup"><span data-stu-id="35324-107">If you have an existing application that has its own account system, or supports other kinds of sign-in from other cloud providers, adding Azure AD sign-in from any tenant is simple.</span></span> <span data-ttu-id="35324-108">只要註冊您的應用程式、透過 OAuth2、OpenID Connect 或 SAML 新增登入程式碼，然後將 [使用 Microsoft 登入] 按鈕放在您的應用程式上即可。</span><span class="sxs-lookup"><span data-stu-id="35324-108">Just register your app, add sign-in code via OAuth2, OpenID Connect, or SAML, and put a "Sign In with Microsoft" button on your application.</span></span> <span data-ttu-id="35324-109">按下面的按鈕來深入了解如何將應用程式加上商標。</span><span class="sxs-lookup"><span data-stu-id="35324-109">Click the following button to learn more about branding your application.</span></span>

<span data-ttu-id="35324-110">[![登入按鈕][AAD-Sign-In]][AAD-App-Branding]</span><span class="sxs-lookup"><span data-stu-id="35324-110">[![Sign in button][AAD-Sign-In]][AAD-App-Branding]</span></span>

<span data-ttu-id="35324-111">本文假設您已經熟悉如何為 Azure AD 建置單一租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-111">This article assumes you’re already familiar with building a single tenant application for Azure AD.</span></span>  <span data-ttu-id="35324-112">如果並非如此，請返回[開發人員指南首頁][AAD-Dev-Guide]，然後試試其中一個快速入門！</span><span class="sxs-lookup"><span data-stu-id="35324-112">If you’re not, head back up to the [developer guide homepage][AAD-Dev-Guide] and try one of our quick starts!</span></span>

<span data-ttu-id="35324-113">將您的應用程式轉換成 Azure AD 多租用戶應用程式包含四個簡單的步驟︰</span><span class="sxs-lookup"><span data-stu-id="35324-113">There are four simple steps to convert your application into an Azure AD multi-tenant app:</span></span>

1. <span data-ttu-id="35324-114">將您的應用程式註冊更新成多租用戶</span><span class="sxs-lookup"><span data-stu-id="35324-114">Update your application registration to be multi-tenant</span></span>
2. <span data-ttu-id="35324-115">將您的程式碼更新成將要求傳送給 /common 端點</span><span class="sxs-lookup"><span data-stu-id="35324-115">Update your code to send requests to the /common endpoint</span></span> 
3. <span data-ttu-id="35324-116">將您的程式碼更新成可處理多個簽發者值</span><span class="sxs-lookup"><span data-stu-id="35324-116">Update your code to handle multiple issuer values</span></span>
4. <span data-ttu-id="35324-117">了解使用者和系統管理員的同意意向並進行適當的程式碼變更</span><span class="sxs-lookup"><span data-stu-id="35324-117">Understand user and admin consent and make appropriate code changes</span></span>

<span data-ttu-id="35324-118">讓我們仔細看看每個步驟。</span><span class="sxs-lookup"><span data-stu-id="35324-118">Let’s look at each step in detail.</span></span> <span data-ttu-id="35324-119">您也可以直接跳到[這份多租用戶範例清單][AAD-Samples-MT]。</span><span class="sxs-lookup"><span data-stu-id="35324-119">You can also jump straight to [this list of multi-tenant samples][AAD-Samples-MT].</span></span>

## <a name="update-registration-to-be-multi-tenant"></a><span data-ttu-id="35324-120">將註冊更新成多租用戶</span><span class="sxs-lookup"><span data-stu-id="35324-120">Update registration to be multi-tenant</span></span>
<span data-ttu-id="35324-121">Azure AD 中的 Web 應用程式/API 註冊預設是單一租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-121">By default, web app/API registrations in Azure AD are single tenant.</span></span>  <span data-ttu-id="35324-122">您只要在 [Azure 入口網站][AZURE-portal]中的應用程式註冊內容頁面上，找出 [多租用戶] 切換開關並將它設定為 [是]，即可將您的註冊轉換成多租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-122">You can make your registration multi-tenant by finding the “Multi-Tenanted” switch on the properties page of your application registration in the [Azure portal][AZURE-portal] and setting it to “Yes”.</span></span>

<span data-ttu-id="35324-123">此外請注意，Azure AD 會要求應用程式的「應用程式識別碼 URI」必須具全域唯一性，才能被設定成多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-123">Also note, before an application can be made multi-tenant, Azure AD requires the App ID URI of the application to be globally unique.</span></span> <span data-ttu-id="35324-124">「應用程式識別碼 URI」是其中一種可在通訊協定訊息中識別應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="35324-124">The App ID URI is one of the ways an application is identified in protocol messages.</span></span>  <span data-ttu-id="35324-125">在單一租用戶應用程式中，只要該租用戶內有唯一的應用程式識別碼 URI 就已足夠。</span><span class="sxs-lookup"><span data-stu-id="35324-125">For a single tenant application, it is sufficient for the App ID URI to be unique within that tenant.</span></span>  <span data-ttu-id="35324-126">就多租用戶應用程式而言，該 URI 則必須具全域唯一性，Azure AD 才能在所有租用戶中找到該應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-126">For a multi-tenant application, it must be globally unique so Azure AD can find the application across all tenants.</span></span>  <span data-ttu-id="35324-127">系統會透過要求「應用程式識別碼 URI」必須具有與已驗證的 Azure AD 租用戶網域相符的主機名稱，來強制執行全域唯一性。</span><span class="sxs-lookup"><span data-stu-id="35324-127">Global uniqueness is enforced by requiring the App ID URI to have a host name that matches a verified domain of the Azure AD tenant.</span></span>  <span data-ttu-id="35324-128">例如，如果租用戶的名稱是 contoso.onmicrosoft.com，則有效的「應用程式識別碼 URI」會是 `https://contoso.onmicrosoft.com/myapp`。</span><span class="sxs-lookup"><span data-stu-id="35324-128">For example, if the name of your tenant was contoso.onmicrosoft.com then a valid App ID URI would be `https://contoso.onmicrosoft.com/myapp`.</span></span>  <span data-ttu-id="35324-129">如果租用戶具有已驗證的網域 `contoso.com`，則有效的「應用程式識別碼 URI」也會是 `https://contoso.com/myapp`。</span><span class="sxs-lookup"><span data-stu-id="35324-129">If your tenant had a verified domain of `contoso.com`, then a valid App ID URI would also be `https://contoso.com/myapp`.</span></span>  <span data-ttu-id="35324-130">如果「應用程式識別碼 URI」沒有按照這個模式，將應用程式設定成多租用戶時就會失敗。</span><span class="sxs-lookup"><span data-stu-id="35324-130">Setting an application as multi-tenant will fail if the App ID URI doesn’t follow this pattern.</span></span>

<span data-ttu-id="35324-131">原生用戶端註冊預設即為多租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-131">Native client registrations are multi-tenant by default.</span></span>  <span data-ttu-id="35324-132">您不需要採取任何動作來將原生用戶端應用程式註冊轉換成多租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-132">You don’t need to take any action to make a native client application registration multi-tenant.</span></span>

## <a name="update-your-code-to-send-requests-to-common"></a><span data-ttu-id="35324-133">將您的程式碼更新成將要求傳送給 /common</span><span class="sxs-lookup"><span data-stu-id="35324-133">Update your code to send requests to /common</span></span>
<span data-ttu-id="35324-134">在單一租用戶應用程式中，登入要求會傳送至租用戶的登入端點。</span><span class="sxs-lookup"><span data-stu-id="35324-134">In a single tenant application, sign-in requests are sent to the tenant’s sign-in endpoint.</span></span> <span data-ttu-id="35324-135">例如，以 contoso.onmicrosoft.com 來說，端點會是：</span><span class="sxs-lookup"><span data-stu-id="35324-135">For example, for contoso.onmicrosoft.com the endpoint would be:</span></span>

    https://login.microsoftonline.com/contoso.onmicrosoft.com

<span data-ttu-id="35324-136">傳送給租用戶端點的要求可以讓該租用戶中的使用者 (或來賓) 登入該租用戶中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-136">Requests sent to a tenant’s endpoint can sign in users (or guests) in that tenant to applications in that tenant.</span></span>  <span data-ttu-id="35324-137">使用多租用戶應用程式時，應用程式事先並不知道使用者來自哪個租用戶，因此您無法將要求傳送給租用戶的端點。</span><span class="sxs-lookup"><span data-stu-id="35324-137">With a multi-tenant application, the application doesn’t know up front what tenant the user is from, so you can’t send requests to a tenant’s endpoint.</span></span>  <span data-ttu-id="35324-138">取而代之的是，會將要求傳送給在所有 Azure AD 租用戶進行多工的端點：</span><span class="sxs-lookup"><span data-stu-id="35324-138">Instead, requests are sent to an endpoint that multiplexes across all Azure AD tenants:</span></span>

    https://login.microsoftonline.com/common

<span data-ttu-id="35324-139">當 Azure AD 在 /common 端點收到要求時，它會讓使用者登入，藉此探索使用者來自哪個租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-139">When Azure AD receives a request on the /common endpoint, it signs the user in and as a consequence discovers which tenant the user is from.</span></span>  <span data-ttu-id="35324-140">/common 端點可以與 Azure AD 支援的所有驗證通訊協定搭配使用：OpenID Connect、OAuth 2.0、SAML 2.0 及「WS-同盟」。</span><span class="sxs-lookup"><span data-stu-id="35324-140">The /common endpoint works with all of the authentication protocols supported by Azure AD:  OpenID Connect, OAuth 2.0, SAML 2.0, and WS-Federation.</span></span>

<span data-ttu-id="35324-141">然後，傳給應用程式的登入回應會包含代表使用者的權杖。</span><span class="sxs-lookup"><span data-stu-id="35324-141">The sign-in response to the application then contains a token representing the user.</span></span>  <span data-ttu-id="35324-142">權杖中的簽發者值會告知應用程式該使用者來自哪個租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-142">The issuer value in the token tells an application what tenant the user is from.</span></span>  <span data-ttu-id="35324-143">從 /common 端點傳回回應時，權杖中的簽發者值將會與使用者的租用戶對應。</span><span class="sxs-lookup"><span data-stu-id="35324-143">When a response returns from the /common endpoint, the issuer value in the token will correspond to the user’s tenant.</span></span>  <span data-ttu-id="35324-144">請務必注意，/common 端點不是租用戶，也不是簽發者，而只是一個多工器。</span><span class="sxs-lookup"><span data-stu-id="35324-144">It’s important to note the /common endpoint is not a tenant and is not an issuer, it’s just a multiplexer.</span></span>  <span data-ttu-id="35324-145">使用 /common 時，必須更新您應用程式中用來驗證權杖的邏輯，以便將這一點納入考量。</span><span class="sxs-lookup"><span data-stu-id="35324-145">When using /common, the logic in your application to validate tokens needs to be updated to take this into account.</span></span> 

<span data-ttu-id="35324-146">如先前所述，多租用戶應用程式也應該為使用者提供一致的登入體驗，以遵循 Azure AD 應用程式的商標指導方針。</span><span class="sxs-lookup"><span data-stu-id="35324-146">As mentioned earlier, multi-tenant applications should also provide a consistent sign-in experience for users, following the Azure AD application branding guidelines.</span></span> <span data-ttu-id="35324-147">按下面的按鈕來深入了解如何將應用程式加上商標。</span><span class="sxs-lookup"><span data-stu-id="35324-147">Click the following button to learn more about branding your application.</span></span>

<span data-ttu-id="35324-148">[![登入按鈕][AAD-Sign-In]][AAD-App-Branding]</span><span class="sxs-lookup"><span data-stu-id="35324-148">[![Sign in button][AAD-Sign-In]][AAD-App-Branding]</span></span>

<span data-ttu-id="35324-149">讓我們深入地看一下 /common 端點的使用和您的程式碼實作。</span><span class="sxs-lookup"><span data-stu-id="35324-149">Let’s take a look at the use of the /common endpoint and your code implementation in more detail.</span></span>

## <a name="update-your-code-to-handle-multiple-issuer-values"></a><span data-ttu-id="35324-150">將您的程式碼更新成可處理多個簽發者值</span><span class="sxs-lookup"><span data-stu-id="35324-150">Update your code to handle multiple issuer values</span></span>
<span data-ttu-id="35324-151">Web 應用程式和 Web API 會接收並驗證來自 Azure AD 的權杖。</span><span class="sxs-lookup"><span data-stu-id="35324-151">Web applications and web APIs receive and validate tokens from Azure AD.</span></span>  

> [!NOTE]
> <span data-ttu-id="35324-152">雖然原生用戶端應用程式會要求並接收來自 Azure AD 的權杖，但它們這麼做是為了將權杖傳送給 API 來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="35324-152">While native client applications request and receive tokens from Azure AD, they do so to send them to APIs, where they are validated.</span></span>  <span data-ttu-id="35324-153">原生應用程式不會驗證權杖，而且必須將它們視為不透明。</span><span class="sxs-lookup"><span data-stu-id="35324-153">Native applications do not validate tokens and must treat them as opaque.</span></span>
> 
> 

<span data-ttu-id="35324-154">讓我們看看應用程式如何驗證它從 Azure AD 接收的權杖。</span><span class="sxs-lookup"><span data-stu-id="35324-154">Let’s look at how an application validates tokens it receives from Azure AD.</span></span>  <span data-ttu-id="35324-155">單一租用戶應用程式通常會採用類似以下的端點值：</span><span class="sxs-lookup"><span data-stu-id="35324-155">A single tenant application will normally take an endpoint value like:</span></span>

    https://login.microsoftonline.com/contoso.onmicrosoft.com

<span data-ttu-id="35324-156">然後使用它來建構中繼資料 URL (在此例中為 OpenID Connect)，例如︰</span><span class="sxs-lookup"><span data-stu-id="35324-156">and use it to construct a metadata URL (in this case, OpenID Connect) like:</span></span>

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

<span data-ttu-id="35324-157">以下載用來驗證權杖的兩項關鍵資訊︰租用戶的簽署金鑰和簽發者值。</span><span class="sxs-lookup"><span data-stu-id="35324-157">to download two critical pieces of information that are used to validate tokens:  the tenant’s signing keys and issuer value.</span></span>  <span data-ttu-id="35324-158">每個 Azure AD 租用戶都有具有採用下列格式的唯一簽發者值︰</span><span class="sxs-lookup"><span data-stu-id="35324-158">Each Azure AD tenant has a unique issuer value of the form:</span></span>

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

<span data-ttu-id="35324-159">其中的 GUID 值是租用戶的租用戶識別碼重新命名安全版本。</span><span class="sxs-lookup"><span data-stu-id="35324-159">where the GUID value is the rename-safe version of the tenant ID of the tenant.</span></span>  <span data-ttu-id="35324-160">如果您按一下上方的 `contoso.onmicrosoft.com` 中繼資料連結，您可以在文件中看到此簽發者值。</span><span class="sxs-lookup"><span data-stu-id="35324-160">If you click on the preceding metadata link for `contoso.onmicrosoft.com`, you can see this issuer value in the document.</span></span>

<span data-ttu-id="35324-161">當單一租用戶應用程式驗證權杖時，它會根據中繼資料文件中的簽署金鑰來檢查權杖的簽章。</span><span class="sxs-lookup"><span data-stu-id="35324-161">When a single tenant application validates a token, it checks the signature of the token against the signing keys from the metadata document.</span></span> <span data-ttu-id="35324-162">這可讓它確定權杖中的簽發者值符合中繼資料文件中找到的值。</span><span class="sxs-lookup"><span data-stu-id="35324-162">This allows it to make sure the issuer value in the token matches the one that was found in the metadata document.</span></span>

<span data-ttu-id="35324-163">因為 /common 端點既不對應租用戶也不是簽發者，所以當您檢查 /common 之中繼資料中的簽發者值時，它擁有的是一個樣板化的 URL 而不是實際值︰</span><span class="sxs-lookup"><span data-stu-id="35324-163">Since the /common endpoint doesn’t correspond to a tenant and isn’t an issuer, when you examine the issuer value in the metadata for /common it has a templated URL instead of an actual value:</span></span>

    https://sts.windows.net/{tenantid}/

<span data-ttu-id="35324-164">因此，多租用戶應用程式無法僅透過將中繼資料中的簽發者值與權杖中的 `issuer` 值做比對來驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="35324-164">Therefore, a multi-tenant application can’t validate tokens just by matching the issuer value in the metadata with the `issuer` value in the token.</span></span>  <span data-ttu-id="35324-165">多租用戶應用程式需要有可根據簽發者值的租用戶識別碼部分來決定哪些簽發者值有效、哪些簽發者值無效的邏輯。</span><span class="sxs-lookup"><span data-stu-id="35324-165">A multi-tenant application needs logic to decide which issuer values are valid and which are not, based on the tenant ID portion of the issuer value.</span></span>  

<span data-ttu-id="35324-166">例如，如果多租用戶應用程式只允許從已註冊服務的特定租用戶登入，它就必須檢查權杖中的簽發者值或 `tid` 宣告值，以確認該租用戶在其訂閱者清單中。</span><span class="sxs-lookup"><span data-stu-id="35324-166">For example, if a multi-tenant application only allows sign-in from specific tenants who have signed up for their service, then it must check either the issuer value or the `tid` claim value in the token to make sure that tenant is in their list of subscribers.</span></span>  <span data-ttu-id="35324-167">如果多租用戶應用程式只處理個人而不根據租用戶做出任何存取決策，則它可以完全忽略簽發者值。</span><span class="sxs-lookup"><span data-stu-id="35324-167">If a multi-tenant application only deals with individuals and doesn’t make any access decisions based on tenants, then it can ignore the issuer value altogether.</span></span>

<span data-ttu-id="35324-168">在可於本文結尾的[相關內容](#related-content)一節中的多租用戶範例中，為了讓任何 Azure AD 租用戶都能登入，已將簽發者驗證停用。</span><span class="sxs-lookup"><span data-stu-id="35324-168">In the multi-tenant samples in the [Related Content](#related-content) section at the end of this article, issuer validation is disabled to enable any Azure AD tenant to sign in.</span></span>

<span data-ttu-id="35324-169">現在，讓我們看看登入多租用戶應用程式之使用者的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="35324-169">Now let’s look at the user experience for users that are signing in to multi-tenant applications.</span></span>

## <a name="understanding-user-and-admin-consent"></a><span data-ttu-id="35324-170">了解使用者和系統管理員的同意意向</span><span class="sxs-lookup"><span data-stu-id="35324-170">Understanding user and admin consent</span></span>
<span data-ttu-id="35324-171">若要讓使用者登入 Azuer AD 中的應用程式，必須以使用者的租用戶代表該應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-171">For a user to sign in to an application in Azure AD, the application must be represented in the user’s tenant.</span></span>  <span data-ttu-id="35324-172">這可讓組織執行一些操作，例如在來自其租用戶的使用者登入應用程式時套用唯一原則。</span><span class="sxs-lookup"><span data-stu-id="35324-172">This allows the organization to do things like apply unique policies when users from their tenant sign in to the application.</span></span>  <span data-ttu-id="35324-173">就單一租用戶應用程式而言，這個註冊程序相當簡單；就是您在 [Azure 入口網站][AZURE-portal]中註冊應用程式時所進行的程序。</span><span class="sxs-lookup"><span data-stu-id="35324-173">For a single tenant application, this registration is simple; it’s the one that happens when you register the application in the [Azure portal][AZURE-portal].</span></span>

<span data-ttu-id="35324-174">就多租用戶應用程式而言，應用程式的初始註冊程序則是在開發人員所使用的 Azure AD 租用戶中進行。</span><span class="sxs-lookup"><span data-stu-id="35324-174">For a multi-tenant application, the initial registration for the application lives in the Azure AD tenant used by the developer.</span></span>  <span data-ttu-id="35324-175">當來自不同租用戶的使用者第一次登入應用程式時，Azure AD 會要求他們同意應用程式所要求的權限。</span><span class="sxs-lookup"><span data-stu-id="35324-175">When a user from a different tenant signs in to the application for the first time, Azure AD asks them to consent to the permissions requested by the application.</span></span>  <span data-ttu-id="35324-176">如果他們同意，系統就會在使用者的租用戶中建立一個稱為「服務主體」的應用程式代表，然後登入便可繼續進行。</span><span class="sxs-lookup"><span data-stu-id="35324-176">If they consent, then a representation of the application called a *service principal* is created in the user’s tenant, and sign-in can continue.</span></span> <span data-ttu-id="35324-177">系統也會在記錄使用者對應用程式之同意意向的目錄中建立委派。</span><span class="sxs-lookup"><span data-stu-id="35324-177">A delegation is also created in the directory that records the user’s consent to the application.</span></span> <span data-ttu-id="35324-178">如需有關應用程式之「應用程式」和「服務主體」物件的詳細資訊，請參閱[應用程式物件和服務主體物件][AAD-App-SP-Objects]。</span><span class="sxs-lookup"><span data-stu-id="35324-178">See [Application Objects and Service Principal Objects][AAD-App-SP-Objects] for details on the application's Application and ServicePrincipal objects, and how they relate to each other.</span></span>

![同意單層式應用程式][Consent-Single-Tier] 

<span data-ttu-id="35324-180">這個同意體驗會受到應用程式所要求的權限影響。</span><span class="sxs-lookup"><span data-stu-id="35324-180">This consent experience is affected by the permissions requested by the application.</span></span>  <span data-ttu-id="35324-181">Azure AD 支援兩種類型的權限，即僅限應用程式的權限和委派的權限︰</span><span class="sxs-lookup"><span data-stu-id="35324-181">Azure AD supports two kinds of permissions, app-only and delegated:</span></span>

* <span data-ttu-id="35324-182">委派的權限可讓應用程式能夠充當登入的使用者來執行該使用者所能執行的一部分操作。</span><span class="sxs-lookup"><span data-stu-id="35324-182">A delegated permission grants an application the ability to act as a signed in user for a subset of the things the user can do.</span></span>  <span data-ttu-id="35324-183">例如，您可以授與應用程式委派的權限來讀取登入之使用者的行事曆。</span><span class="sxs-lookup"><span data-stu-id="35324-183">For example, you can grant an application the delegated permission to read the signed in user’s calendar.</span></span>
* <span data-ttu-id="35324-184">僅限應用程式的權限會直接授與應用程式的識別身分。</span><span class="sxs-lookup"><span data-stu-id="35324-184">An app-only permission is granted directly to the identity of the application.</span></span>  <span data-ttu-id="35324-185">例如，您可以將僅限應用程式的權限授與應用程式來讀取租用戶中的使用者清單，而且不論是誰登入此應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-185">For example, you can grant an application the app-only permission to read the list of users in a tenant, regardless of who is signed in to the application.</span></span>

<span data-ttu-id="35324-186">有些權限可以由一般使用者同意，有些則需要租用戶系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="35324-186">Some permissions can be consented to by a regular user, while others require a tenant administrator’s consent.</span></span> 

### <a name="admin-consent"></a><span data-ttu-id="35324-187">系統管理員同意</span><span class="sxs-lookup"><span data-stu-id="35324-187">Admin consent</span></span>
<span data-ttu-id="35324-188">僅限應用程式的權限一律需要租用戶系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="35324-188">App-only permissions always require a tenant administrator’s consent.</span></span>  <span data-ttu-id="35324-189">如果您的應用程式要求僅限應用程式的權限，當使用者嘗試登入應用程式時，將會出現錯誤訊息，指出該使用者無法同意。</span><span class="sxs-lookup"><span data-stu-id="35324-189">If your application requests an app-only permission and a user tries to sign in to the application, an error message will be displayed saying the user isn’t able to consent.</span></span>

<span data-ttu-id="35324-190">有些委派的權限也需要租用戶系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="35324-190">Certain delegated permissions also require a tenant administrator’s consent.</span></span>  <span data-ttu-id="35324-191">例如，若要能夠以登入的使用者身分寫回 Azure AD，就需要租用戶系統管理員的同意。</span><span class="sxs-lookup"><span data-stu-id="35324-191">For example, the ability to write back to Azure AD as the signed in user requires a tenant administrator’s consent.</span></span>  <span data-ttu-id="35324-192">與僅限應用程式的權限一樣，如果一般使用者嘗試登入要求委派權限的應用程式，而該權限需要系統管理員同意，您的應用程式將會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="35324-192">Like app-only permissions, if an ordinary user tries to sign in to an application that requests a delegated permission that requires administrator consent, your application will receive an error.</span></span>  <span data-ttu-id="35324-193">權限是否需要系統管理員同意是由發佈資源的開發人員決定，而且可以在該資源的文件中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="35324-193">Whether or not a permission requires admin consent is determined by the developer that published the resource, and can be found in the documentation for the resource.</span></span>  <span data-ttu-id="35324-194">如需說明 Azure AD Graph API 和 Microsoft Graph API 可用權限的主題連結，請參閱本文的 [相關內容](#related-content) 一節。</span><span class="sxs-lookup"><span data-stu-id="35324-194">Links to topics describing the available permissions for the Azure AD Graph API and Microsoft Graph API are in the [Related Content](#related-content) section of this article.</span></span>

<span data-ttu-id="35324-195">如果您的應用程式使用需要系統管理員同意的權限，您就必須要有相關的表示，例如可供系統管理員起始動作的按鈕或連結。</span><span class="sxs-lookup"><span data-stu-id="35324-195">If your application uses permissions that require admin consent, you need to have a gesture such as a button or link where the admin can initiate the action.</span></span>  <span data-ttu-id="35324-196">您的應用程式針對此動作傳送的要求是一個一般的 OAuth2/OpenID Connect 授權要求，但此要求同時也包含 `prompt=admin_consent` 查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="35324-196">The request your application sends for this action is a usual OAuth2/OpenID Connect authorization request, but that also includes the `prompt=admin_consent` query string parameter.</span></span>  <span data-ttu-id="35324-197">在系統管理員同意且系統已在客戶的租用戶中建立服務主體之後，後續的登入要求就不再需要 `prompt=admin_consent` 參數。</span><span class="sxs-lookup"><span data-stu-id="35324-197">Once the admin has consented and the service principal is created in the customer’s tenant, subsequent sign-in requests do not need the `prompt=admin_consent` parameter.</span></span> <span data-ttu-id="35324-198">由於系統管理員已決定可接受要求的權限，因此從該時間點之後，就不會再提示租用戶中的任何其他使用者行使同意權。</span><span class="sxs-lookup"><span data-stu-id="35324-198">Since the administrator has decided the requested permissions are acceptable, no other users in the tenant will be prompted for consent from that point forward.</span></span>

<span data-ttu-id="35324-199">如果應用程式要求的權限不需要系統管理員同意，則應用程式也可以使用 `prompt=admin_consent` 參數。</span><span class="sxs-lookup"><span data-stu-id="35324-199">The `prompt=admin_consent` parameter can also be used by applications that request permissions that do not require admin consent.</span></span> <span data-ttu-id="35324-200">這是在應用程式需要一種體驗的情況下完成，也就是租用戶系統管理員「註冊」一次，此後就不會再提示其他使用者要表示同意。</span><span class="sxs-lookup"><span data-stu-id="35324-200">This is done when the applicaton requires an experience where the tenant admin “signs up” one time, and no other users are prompted for consent from that point on.</span></span>

<span data-ttu-id="35324-201">如果應用程式需要系統管理員同意，當系統管理員登入，但未傳送 `prompt=admin_consent` 參數時，系統管理員**只針對其使用者帳戶**才會順利同意此應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-201">If an application requires admin consent, and an admin signs in but the `prompt=admin_consent` parameter is not sent, the admin will successfully consent to the application **only for their user account**.</span></span>  <span data-ttu-id="35324-202">一般使用者將仍然無法登入此應用程式並對其行使同意權。</span><span class="sxs-lookup"><span data-stu-id="35324-202">Regular users will still not be able to sign in and consent to the application.</span></span>  <span data-ttu-id="35324-203">當您想要先讓租用戶系統管理員能夠瀏覽您的應用程式，然後才允許其他使用者存取時，這會相當有用。</span><span class="sxs-lookup"><span data-stu-id="35324-203">This is useful if you want to give the tenant administrator the ability to explore your application before allowing other users access.</span></span>

<span data-ttu-id="35324-204">租用戶系統管理員可以停用一般使用者對應用程式行使同意權的能力。</span><span class="sxs-lookup"><span data-stu-id="35324-204">A tenant administrator can disable the ability for regular users to consent to applications.</span></span>  <span data-ttu-id="35324-205">如果停用這項功能，就一律需要系統管理員同意，才能在租用戶中設定應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-205">If this capability is disabled, admin consent is always required for the application to be set up in the tenant.</span></span>  <span data-ttu-id="35324-206">如果您想要在停用一般使用者同意的情況下測試您的應用程式，您可以在 [Azure 入口網站][AZURE-portal]的 Azure AD 租用戶設定區段中找到設定參數。</span><span class="sxs-lookup"><span data-stu-id="35324-206">If you want to test your application with regular user consent disabled, you can find the configuration switch in the Azure AD tenant configuration section of the [Azure portal][AZURE-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="35324-207">有些應用程式想要提供一種體驗，讓一般使用者能夠一開始即表示同意，之後應用程式即可讓系統管理員參與操作並要求需要系統管理員同意的權限。</span><span class="sxs-lookup"><span data-stu-id="35324-207">Some applications want an experience where regular users are able to consent initially, and later the application can involve the administrator and request permissions that require admin consent.</span></span>  <span data-ttu-id="35324-208">目前在 Azure AD 中還沒有任何方法可以使用單一應用程式註冊來達到這個目的。</span><span class="sxs-lookup"><span data-stu-id="35324-208">There is no way to do this with a single application registration in Azure AD today.</span></span>  <span data-ttu-id="35324-209">即將推出 Azure AD v2 端點將可允許應用程式在執行階段 (而不是在註冊階段) 要求權限，這將使得此情況變成可行。</span><span class="sxs-lookup"><span data-stu-id="35324-209">The upcoming Azure AD v2 endpoint will allow applications to request permissions at runtime, instead of at registration time, which will enable this scenario.</span></span>  <span data-ttu-id="35324-210">如需詳細資訊，請參閱 [Azure AD 應用程式模型 v2 開發人員指南][AAD-V2-Dev-Guide]。</span><span class="sxs-lookup"><span data-stu-id="35324-210">For more information, see the [Azure AD App Model v2 Developer Guide][AAD-V2-Dev-Guide].</span></span>
> 
> 

### <a name="consent-and-multi-tier-applications"></a><span data-ttu-id="35324-211">同意和多層應用程式</span><span class="sxs-lookup"><span data-stu-id="35324-211">Consent and multi-tier applications</span></span>
<span data-ttu-id="35324-212">您的應用程式可能會有多層，每一層皆由它自己在 Azure AD 中的註冊代表。</span><span class="sxs-lookup"><span data-stu-id="35324-212">Your application may have multiple tiers, each represented by its own registration in Azure AD.</span></span>  <span data-ttu-id="35324-213">例如，一個呼叫 Web API 的原生應用程式，或是一個呼叫 Web API 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-213">For example, a native application that calls a web API, or a web application that calls a web API.</span></span>  <span data-ttu-id="35324-214">在這兩種情況下，用戶端 (原生應用程式或 Web 應用程式) 都會要求可呼叫資源 (Web API) 的權限。</span><span class="sxs-lookup"><span data-stu-id="35324-214">In both of these cases, the client (native app or web app) requests permissions to call the resource (web API).</span></span>  <span data-ttu-id="35324-215">若要讓用戶端順利獲得客戶同意新增到其租用戶中，則它要求權限的所有資源必須都已經存在於客戶的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="35324-215">For the client to be successfully consented into a customer’s tenant, all resources to which it requests permissions must already exist in the customer’s tenant.</span></span>  <span data-ttu-id="35324-216">如果不符合此條件，Azuer AD 將會傳回錯誤，指出必須先新增資源。</span><span class="sxs-lookup"><span data-stu-id="35324-216">If this condition isn’t met, Azure AD will return an error that the resource must be added first.</span></span>

<span data-ttu-id="35324-217">**單一租用戶中的多層**</span><span class="sxs-lookup"><span data-stu-id="35324-217">**Multiple tiers in a single tenant**</span></span>

<span data-ttu-id="35324-218">如果您的邏輯應用程式包含兩個或更多個應用程式註冊 (例如個別的用戶端和資源)，這可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="35324-218">This can be a problem if your logical application consists of two or more application registrations, for example a separate client and resource.</span></span>  <span data-ttu-id="35324-219">如何先將資源新增到客戶租用戶中？</span><span class="sxs-lookup"><span data-stu-id="35324-219">How do you get the resource into the customer tenant first?</span></span>  <span data-ttu-id="35324-220">Azure AD 涵蓋此情況，支援在單一步驟中同意用戶端和資源。</span><span class="sxs-lookup"><span data-stu-id="35324-220">Azure AD covers this case by enabling client and resource to be consented in a single step.</span></span> <span data-ttu-id="35324-221">使用者在同意頁面上會看到用戶端和資源所要求的權限總和。</span><span class="sxs-lookup"><span data-stu-id="35324-221">The user sees the sum total of the permissions requested by both the client and resource on the consent page.</span></span>  <span data-ttu-id="35324-222">若要啟用此行為，在資源的應用程式資訊清單中，資源的應用程式註冊就必須以 `knownClientApplications` 的形式包含用戶端的「應用程式識別碼」。</span><span class="sxs-lookup"><span data-stu-id="35324-222">To enable this behavior, the resource’s application registration must include the client’s App ID as a `knownClientApplications` in its application manifest.</span></span>  <span data-ttu-id="35324-223">例如：</span><span class="sxs-lookup"><span data-stu-id="35324-223">For example:</span></span>

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

<span data-ttu-id="35324-224">您可以透過資源[應用程式的資訊清單][AAD-App-Manifest]更新此屬性。</span><span class="sxs-lookup"><span data-stu-id="35324-224">This property can be updated via the resource [application’s manifest][AAD-App-Manifest].</span></span> <span data-ttu-id="35324-225">在本文結尾的[相關內容](#related-content)一節中，一個呼叫 Web API 的多層原生用戶端範例中會示範作法。</span><span class="sxs-lookup"><span data-stu-id="35324-225">This is demonstrated in a multi-tier native client calling web API sample in the [Related Content](#related-content) section at the end of this article.</span></span> <span data-ttu-id="35324-226">下圖提供同意單一租用戶中註冊之多層應用程式的概觀︰</span><span class="sxs-lookup"><span data-stu-id="35324-226">The following diagram provides an overview of consent for a multi-tier app registered in a single tenant :</span></span>

![同意多層式已知用戶端應用程式][Consent-Multi-Tier-Known-Client] 

<span data-ttu-id="35324-228">**多個租用戶中的多層**</span><span class="sxs-lookup"><span data-stu-id="35324-228">**Multiple tiers in multiple tenants**</span></span>

<span data-ttu-id="35324-229">如果在不同的租用戶中註冊不同的應用程式層，將會發生類似的情況。</span><span class="sxs-lookup"><span data-stu-id="35324-229">A similar case happens if the different tiers of an application are registered in different tenants.</span></span>  <span data-ttu-id="35324-230">例如，想像建置一個會呼叫 Office 365 Exchange Online API 的原生用戶端應用程式的情況。</span><span class="sxs-lookup"><span data-stu-id="35324-230">For example, consider the case of building a native client application that calls the Office 365 Exchange Online API.</span></span>  <span data-ttu-id="35324-231">若要開發此原生應用程式，然後讓此原生應用程式在客戶的租用戶中執行，就必須要有 Exchange Online 服務主體。</span><span class="sxs-lookup"><span data-stu-id="35324-231">To develop the native application, and later for the native application to run in a customer’s tenant, the Exchange Online service principal must be present.</span></span>  <span data-ttu-id="35324-232">在此情況下，開發人員和客戶必須購買 Exchange Online，如此才能在其租用戶中建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="35324-232">In this case, the developer and customer must purchase Exchange Online for the service principal to be created in their tenants.</span></span>  

<span data-ttu-id="35324-233">如果是 Microsoft 以外的組織所建置的 API，API 的開發人員必須提供方法讓客戶同意將應用程式新增至其客戶的租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-233">In the case of an API built by an organization other than Microsoft, the developer of the API needs to provide a way for their customers to consent the application into their customers' tenants.</span></span> <span data-ttu-id="35324-234">建議的設計是第三方開發人員將 API 建置成也可當作 Web 用戶端來實作註冊︰</span><span class="sxs-lookup"><span data-stu-id="35324-234">The recommended design is for the 3rd party developer to build the API such that it can also function as a web client to implement sign-up :</span></span>

1. <span data-ttu-id="35324-235">遵循先前的章節，以確保 API 實作多租用戶應用程式註冊/程式碼的需求</span><span class="sxs-lookup"><span data-stu-id="35324-235">Follow the earlier sections to ensure the API implements the multi-tenant application registration/code requirements</span></span>
2. <span data-ttu-id="35324-236">除了公開 API 的範圍/角色，請確定註冊包含「登入和讀取使用者設定檔」Azure AD 權限 (依預設會提供)</span><span class="sxs-lookup"><span data-stu-id="35324-236">In addition to exposing the API's scopes/roles, ensure the registration includes the "Sign in and read user profile" Azure AD permission (provided by default)</span></span>
3. <span data-ttu-id="35324-237">遵循稍早討論的[系統管理員同意](#admin-consent)指引，在 Web 用戶端實作登入/註冊頁面</span><span class="sxs-lookup"><span data-stu-id="35324-237">Implement a sign-in/sign-up page in the web client, following the [admin consent](#admin-consent) guidance discussed earlier</span></span> 
4. <span data-ttu-id="35324-238">當使用者同意應用程式後，就會在其租用戶中會建立服務主體和同意委派連結，而原生應用程式可以取得 API 的權杖</span><span class="sxs-lookup"><span data-stu-id="35324-238">Once the user consents to the application, the service principal and consent delegation links are created in their tenant, and the native application can get tokens for the API</span></span>

<span data-ttu-id="35324-239">下圖提供同意不同租用戶中註冊之多層應用程式的概觀︰</span><span class="sxs-lookup"><span data-stu-id="35324-239">The following diagram provides an overview of consent for a multi-tier app registered in different tenants:</span></span>

![同意多層式多方應用程式][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a><span data-ttu-id="35324-241">撤銷同意</span><span class="sxs-lookup"><span data-stu-id="35324-241">Revoking Consent</span></span>
<span data-ttu-id="35324-242">使用者和系統管理員可以隨時撤銷對您應用程式的同意：</span><span class="sxs-lookup"><span data-stu-id="35324-242">Users and administrators can revoke consent to your application at any time:</span></span>

* <span data-ttu-id="35324-243">使用者可藉由將個別應用程式從其[存取面板應用程式][AAD-Access-Panel]清單中移除，來撤銷對這些應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="35324-243">Users revoke access to individual applications by removing them from their [Access Panel Applications][AAD-Access-Panel] list.</span></span>
* <span data-ttu-id="35324-244">系統管理員可藉由使用 [Azure 入口網站][AZURE-portal]的 Azure AD 管理區段，將應用程式從 Azure AD 中移除，來撤銷對這些應用程式的存取權。</span><span class="sxs-lookup"><span data-stu-id="35324-244">Administrators revoke access to applications by removing them from Azure AD using the Azure AD management section of the [Azure portal][AZURE-portal].</span></span>

<span data-ttu-id="35324-245">如果是由系統管理員代表租用戶中的所有使用者對應用程式行使同意權，使用者就不能個別撤銷存取權。</span><span class="sxs-lookup"><span data-stu-id="35324-245">If an administrator consents to an application for all users in a tenant, users cannot revoke access individually.</span></span>  <span data-ttu-id="35324-246">只有系統管理員才能撤銷存取權，並且只能針對整個應用程式撤銷。</span><span class="sxs-lookup"><span data-stu-id="35324-246">Only the administrator can revoke access, and only for the whole application.</span></span>

### <a name="consent-and-protocol-support"></a><span data-ttu-id="35324-247">同意和通訊協定支援</span><span class="sxs-lookup"><span data-stu-id="35324-247">Consent and Protocol Support</span></span>
<span data-ttu-id="35324-248">在 Azure AD 中，是透過 OAuth、OpenID Connect、「WS-同盟」及 SAML 通訊協定來支援同意。</span><span class="sxs-lookup"><span data-stu-id="35324-248">Consent is supported in Azure AD via the OAuth, OpenID Connect, WS-Federation, and SAML protocols.</span></span>  <span data-ttu-id="35324-249">由於 SAML 和「WS-同盟」通訊協定並不支援 `prompt=admin_consent` 參數，因此系統管理員只能透過 OAuth 和 OpenID Connect 行使同意權。</span><span class="sxs-lookup"><span data-stu-id="35324-249">The SAML and WS-Federation protocols do not support the `prompt=admin_consent` parameter, so admin consent is only possible via OAuth and OpenID Connect.</span></span>

## <a name="multi-tenant-applications-and-caching-access-tokens"></a><span data-ttu-id="35324-250">多租用戶應用程式和快取存取權杖</span><span class="sxs-lookup"><span data-stu-id="35324-250">Multi-Tenant Applications and Caching Access Tokens</span></span>
<span data-ttu-id="35324-251">多租用戶應用程式也可以取得存取權杖來呼叫受 Azure AD 保護的 API。</span><span class="sxs-lookup"><span data-stu-id="35324-251">Multi-tenant applications can also get access tokens to call APIs that are protected by Azure AD.</span></span>  <span data-ttu-id="35324-252">搭配多租用戶應用程式使用 Active Directory Authentication Library (ADAL) 時有一個常見的錯誤，就是一開始即使用 /common 來為使用者要求權杖、接收回應，然後也使用 /common 來為該相同使用者要求後續的權杖。</span><span class="sxs-lookup"><span data-stu-id="35324-252">A common error when using the Active Directory Authentication Library (ADAL) with a multi-tenant application, is to initially request a token for a user using /common, receive a response, then request a subsequent token for that same user also using /common.</span></span>  <span data-ttu-id="35324-253">由於從 Azure AD 傳回的回應是來自租用戶而非 /common，因此 ADAL 快取權杖時會將它視為來自租用戶。</span><span class="sxs-lookup"><span data-stu-id="35324-253">Since the response from Azure AD comes from a tenant, not /common, ADAL caches the token as being from the tenant.</span></span> <span data-ttu-id="35324-254">後續為了為使用者取得存取權杖而進行的 /common 呼叫會遺漏快取項目，因此系統會再次提示使用者登入。</span><span class="sxs-lookup"><span data-stu-id="35324-254">The subsequent call to /common to get an access token for the user misses the cache entry, and the user is prompted to sign in again.</span></span>  <span data-ttu-id="35324-255">為了避免遺漏快取，請確定後續為已登入之使用者進行的呼叫是對租用戶的端點發出。</span><span class="sxs-lookup"><span data-stu-id="35324-255">To avoid missing the cache, make sure subsequent calls for an already signed in user are made to the tenant’s endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35324-256">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35324-256">Next steps</span></span>
<span data-ttu-id="35324-257">在本文中，您已了解如何建置可讓使用者從任何 Azure Active Directory 租用戶登入的應用程式。</span><span class="sxs-lookup"><span data-stu-id="35324-257">In this article, you learned how to build an application that can sign in a user from any Azure Active Directory tenant.</span></span> <span data-ttu-id="35324-258">在啟用您應用程式與 Azure Active Directory 之間的單一登入功能之後，您也可以將應用程式更新成存取 Microsoft 資源 (例如 Office 365) 所公開的 API。</span><span class="sxs-lookup"><span data-stu-id="35324-258">After enabling Single Sign-On between your app and Azure Active Directory, you can also update your application to access APIs exposed by Microsoft resources, like Office 365.</span></span> <span data-ttu-id="35324-259">因此，您可以在應用程式中提供個人化的體驗，例如向使用者顯示內容資訊，像是他們的個人資料圖片或下一個行事曆約會。</span><span class="sxs-lookup"><span data-stu-id="35324-259">So you can offer a personalized experience in your application, for example showing contextual information to the users, like their profile picture or their next calendar appointment.</span></span> <span data-ttu-id="35324-260">若要深入了解如何對 Azure Active Directory 和 Office 365 服務 (例如 Exchange、SharePoint、OneDrive、OneNote、Planner、Excel 等) 進行 API 呼叫，請瀏覽：[Microsoft Graph API][MSFT-Graph-overview]。</span><span class="sxs-lookup"><span data-stu-id="35324-260">To learn more about making API calls to Azure Active Directory and Office 365 services like Exchange, SharePoint, OneDrive, OneNote, Planner, Excel and more, visit: [Microsoft Graph API][MSFT-Graph-overview].</span></span>


## <a name="related-content"></a><span data-ttu-id="35324-261">相關內容</span><span class="sxs-lookup"><span data-stu-id="35324-261">Related content</span></span>
* <span data-ttu-id="35324-262">[多租用戶應用程式範例][AAD-Samples-MT]</span><span class="sxs-lookup"><span data-stu-id="35324-262">[Multi-tenant application samples][AAD-Samples-MT]</span></span>
* <span data-ttu-id="35324-263">[應用程式的商標指導方針][AAD-App-Branding]</span><span class="sxs-lookup"><span data-stu-id="35324-263">[Branding Guidelines for Applications][AAD-App-Branding]</span></span>
* <span data-ttu-id="35324-264">[Azure AD 開發人員指南][AAD-Dev-Guide]</span><span class="sxs-lookup"><span data-stu-id="35324-264">[Azure AD Developer's Guide][AAD-Dev-Guide]</span></span>
* <span data-ttu-id="35324-265">[應用程式物件和服務主體物件][AAD-App-SP-Objects]</span><span class="sxs-lookup"><span data-stu-id="35324-265">[Application Objects and Service Principal Objects][AAD-App-SP-Objects]</span></span>
* <span data-ttu-id="35324-266">[整合應用程式與 Azure Active Directory][AAD-Integrating-Apps]</span><span class="sxs-lookup"><span data-stu-id="35324-266">[Integrating Applications with Azure Active Directory][AAD-Integrating-Apps]</span></span>
* <span data-ttu-id="35324-267">[同意架構的概觀][AAD-Consent-Overview]</span><span class="sxs-lookup"><span data-stu-id="35324-267">[Overview of the Consent Framework][AAD-Consent-Overview]</span></span>
* <span data-ttu-id="35324-268">[Microsoft Graph API 權限範圍][MSFT-Graph-permision-scopes]</span><span class="sxs-lookup"><span data-stu-id="35324-268">[Microsoft Graph API Permission Scopes][MSFT-Graph-permision-scopes]</span></span>
* <span data-ttu-id="35324-269">[Azure AD Graph API 權限範圍][AAD-Graph-Perm-Scopes]</span><span class="sxs-lookup"><span data-stu-id="35324-269">[Azure AD Graph API Permission Scopes][AAD-Graph-Perm-Scopes]</span></span>

<span data-ttu-id="35324-270">請使用下列意見區段來提供意見反應，並協助我們改善及設計我們的內容。</span><span class="sxs-lookup"><span data-stu-id="35324-270">Please use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














