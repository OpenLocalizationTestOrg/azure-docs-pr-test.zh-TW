---
title: "Azure Active Directory 驗證和 Resource Manager | Microsoft Docs"
description: "使用 Azure Resource Manager API 與 Azure Active Directory 進行驗證以整合應用程式與其他 Azure 訂用帳戶的開發人員指南。"
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 7830dc4774652f4d108e98660dce3bcea7b32d05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-resource-manager-authentication-api-to-access-subscriptions"></a><span data-ttu-id="eebc1-103">使用 Resource Manager 驗證 API 來存取訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="eebc1-103">Use Resource Manager authentication API to access subscriptions</span></span>
## <a name="introduction"></a><span data-ttu-id="eebc1-104">簡介</span><span class="sxs-lookup"><span data-stu-id="eebc1-104">Introduction</span></span>
<span data-ttu-id="eebc1-105">如果您是必須建立應用程式來管理客戶的 Azure 資源的軟體開發人員，本主題說明如何使用 Azure Resource Manager API 來進行驗證，並取得其他訂用帳戶中資源的存取權。</span><span class="sxs-lookup"><span data-stu-id="eebc1-105">If you are a software developer who needs to create an app that manages customer's Azure resources, this topic shows you how to authenticate with the Azure Resource Manager APIs and gain access to resources in other subscriptions.</span></span>

<span data-ttu-id="eebc1-106">您的應用程式可透過數種方式存取資源管理員 API︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-106">Your app can access the Resource Manager APIs in couple of ways:</span></span>

1. <span data-ttu-id="eebc1-107">**使用者 + 應用程式存取**︰適用於代表登入使用者存取資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-107">**User + app access**: for apps that access resources on behalf of a signed-in user.</span></span> <span data-ttu-id="eebc1-108">此方式適用於僅處理「互動式管理」Azure 資源的應用程式，例如 Web 應用程式和命令列工具。</span><span class="sxs-lookup"><span data-stu-id="eebc1-108">This approach works for apps, such as web apps and command-line tools, that deal with only "interactive management" of Azure resources.</span></span>
2. <span data-ttu-id="eebc1-109">**僅限應用程式存取**︰適用於執行協助程式服務和已排程之作業的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-109">**App-only access**: for apps that run daemon services and scheduled jobs.</span></span> <span data-ttu-id="eebc1-110">應用程式的身分識別會獲得資源的直接存取權。</span><span class="sxs-lookup"><span data-stu-id="eebc1-110">The app's identity is granted direct access to the resources.</span></span> <span data-ttu-id="eebc1-111">此方式適用於需要長期無周邊 (自動) 存取 Azure 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-111">This approach works for apps that need long-term headless (unattended) access to Azure.</span></span>

<span data-ttu-id="eebc1-112">本主題提供建立應用程式來運用這兩種授權方法的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="eebc1-112">This topic provides step-by-step instructions to create an app that employs both these authorization methods.</span></span> <span data-ttu-id="eebc1-113">它會說明如何使用 REST API 或 C# 執行每個步驟。</span><span class="sxs-lookup"><span data-stu-id="eebc1-113">It shows how to perform each step with REST API or C#.</span></span> <span data-ttu-id="eebc1-114">完整的 ASP.NET MVC 應用程式可在 [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense)取得。</span><span class="sxs-lookup"><span data-stu-id="eebc1-114">The complete ASP.NET MVC application is available at [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).</span></span>

## <a name="what-the-web-app-does"></a><span data-ttu-id="eebc1-115">Web 應用程式的功用</span><span class="sxs-lookup"><span data-stu-id="eebc1-115">What the web app does</span></span>
<span data-ttu-id="eebc1-116">Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="eebc1-116">The web app:</span></span>

1. <span data-ttu-id="eebc1-117">登入 Azure 使用者。</span><span class="sxs-lookup"><span data-stu-id="eebc1-117">Signs-in an Azure user.</span></span>
2. <span data-ttu-id="eebc1-118">要求使用者授與 Resource Manager 的存取權給 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-118">Asks user to grant the web app access to Resource Manager.</span></span>
3. <span data-ttu-id="eebc1-119">取得使用者 + 應用程式的存取權杖來存取 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="eebc1-119">Gets user + app access token for accessing Resource Manager.</span></span>
4. <span data-ttu-id="eebc1-120">使用權杖 (來自步驟 3) 呼叫 Resource Manager，並將應用程式的服務主體指派給訂用帳戶中的角色，讓應用程式能長期存取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-120">Uses token (from step 3) to call Resource Manager and assign the app's service principal to a role in the subscription, which gives the app long-term access to the subscription.</span></span>
5. <span data-ttu-id="eebc1-121">取得僅限應用程式存取權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-121">Gets app-only access token.</span></span>
6. <span data-ttu-id="eebc1-122">使用權杖 (來自步驟 5) 以透過 Resource Manager 管理訂用帳戶中的資源。</span><span class="sxs-lookup"><span data-stu-id="eebc1-122">Uses token (from step 5) to manage resources in the subscription through Resource Manager.</span></span>

<span data-ttu-id="eebc1-123">以下是 Web 應用程式的端對端流程。</span><span class="sxs-lookup"><span data-stu-id="eebc1-123">Here's the end-to-end flow of the web application.</span></span>

![Resource Manager 驗證流程](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

<span data-ttu-id="eebc1-125">身為使用者，您必須提供所要使用之訂用帳戶的訂用帳戶識別碼︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-125">As a user, you provide the subscription id for the subscription you want to use:</span></span>

![提供訂用帳戶識別碼](./media/resource-manager-api-authentication/sample-ux-1.png)

<span data-ttu-id="eebc1-127">選取要用於登入的帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-127">Select the account to use for logging in.</span></span>

![選取帳戶](./media/resource-manager-api-authentication/sample-ux-2.png)

<span data-ttu-id="eebc1-129">提供您的認證。</span><span class="sxs-lookup"><span data-stu-id="eebc1-129">Provide your credentials.</span></span>

![提供認證](./media/resource-manager-api-authentication/sample-ux-3.png)

<span data-ttu-id="eebc1-131">授與應用程式存取您的 Azure 訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-131">Grant the app access to your Azure subscriptions:</span></span>

![授與存取權](./media/resource-manager-api-authentication/sample-ux-4.png)

<span data-ttu-id="eebc1-133">管理連接的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="eebc1-133">Manage your connected subscriptions:</span></span>

![連線訂用帳戶](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a><span data-ttu-id="eebc1-135">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="eebc1-135">Register application</span></span>
<span data-ttu-id="eebc1-136">在開始撰寫程式碼之前，請先使用 Azure Active Directory (AD) 註冊 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-136">Before you start coding, register your web app with Azure Active Directory (AD).</span></span> <span data-ttu-id="eebc1-137">應用程式註冊會為您在 Azure AD 中的應用程式建立中央身分識別。</span><span class="sxs-lookup"><span data-stu-id="eebc1-137">The app registration creates a central identity for your app in Azure AD.</span></span> <span data-ttu-id="eebc1-138">它會保留您的應用程式的基本資訊，例如您的應用程式用來驗證和存取 Azure Resource Manager API 的 OAuth 用戶端識別碼、回覆 URL 和認證。</span><span class="sxs-lookup"><span data-stu-id="eebc1-138">It holds basic information about your application like OAuth Client ID, Reply URLs, and credentials that your application uses to authenticate and access Azure Resource Manager APIs.</span></span> <span data-ttu-id="eebc1-139">應用程式註冊也會記錄您的應用程式需要的各種委派權限，以便代表使用者存取 Microsoft API。</span><span class="sxs-lookup"><span data-stu-id="eebc1-139">The app registration also records the various delegated permissions that your application needs when accessing Microsoft APIs on behalf of the user.</span></span>

<span data-ttu-id="eebc1-140">由於應用程式會存取其他訂用帳戶，您必須將它設定為多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-140">Because your app accesses other subscription, you must configure it as a multi-tenant application.</span></span> <span data-ttu-id="eebc1-141">為了通過驗證，請提供與 Azure Active Directory 相關聯的網域。</span><span class="sxs-lookup"><span data-stu-id="eebc1-141">To pass validation, provide a domain associated with your Azure Active Directory.</span></span> <span data-ttu-id="eebc1-142">若要查看與 Azure Active Directory 相關聯的網域，請登入[傳統入口網站 (英文)](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-142">To see the domains associated with your Azure Active Directory, log in to the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="eebc1-143">選取您的 Azure Active Directory，然後選取 [網域]。</span><span class="sxs-lookup"><span data-stu-id="eebc1-143">Select your Azure Active Directory and then select **Domains**.</span></span>

<span data-ttu-id="eebc1-144">下列範例示範如何使用 Azure PowerShell 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-144">The following example shows how to register the app by using Azure PowerShell.</span></span> <span data-ttu-id="eebc1-145">您必須擁有最新版 (2016 年 8 月) Azure PowerShell 才能讓此命令生效。</span><span class="sxs-lookup"><span data-stu-id="eebc1-145">You must have the latest version (August 2016) of Azure PowerShell for this command to work.</span></span>

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

<span data-ttu-id="eebc1-146">若要登入為 AD 應用程式，您需要應用程式的識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-146">To log in as the AD application, you need the application id and password.</span></span> <span data-ttu-id="eebc1-147">若要查看前一個命令所傳回的應用程式識別碼，請使用︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-147">To see the application id that is returned from the previous command, use:</span></span>

    $app.ApplicationId

<span data-ttu-id="eebc1-148">下列範例示範如何使用 Azure CLI 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-148">The following example shows how to register the app by using Azure CLI.</span></span>

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

<span data-ttu-id="eebc1-149">結果內包含 AppId，以應用程式的形式進行驗證時會需要此資料。</span><span class="sxs-lookup"><span data-stu-id="eebc1-149">The results include the AppId, which you need when authenticating as the application.</span></span>

### <a name="optional-configuration---certificate-credential"></a><span data-ttu-id="eebc1-150">選擇性組態 - 憑證認證</span><span class="sxs-lookup"><span data-stu-id="eebc1-150">Optional configuration - certificate credential</span></span>
<span data-ttu-id="eebc1-151">Azure AD 也支援應用程式的憑證認證︰您建立自我簽署憑證、保留私密金鑰，然後將公開金鑰新增至 Azure AD 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="eebc1-151">Azure AD also supports certificate credentials for applications: you create a self-signed cert, keep the private key, and add the public key to your Azure AD application registration.</span></span> <span data-ttu-id="eebc1-152">若為驗證，您的應用程式會使用您的私密金鑰將小裝載傳送至簽署的 Azure AD，且 Azure AD 會使用您註冊的公開金鑰來驗證簽章。</span><span class="sxs-lookup"><span data-stu-id="eebc1-152">For authentication, your application sends a small payload to Azure AD signed using your private key, and Azure AD validates the signature using the public key that you registered.</span></span>

<span data-ttu-id="eebc1-153">如需使用憑證建立 AD 應用程式的相關資訊，請參閱[使用 Azure PowerShell 建立用來存取資源的服務主體](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)或[使用 Azure CLI 建立用來存取資源的服務主體](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-153">For information about creating an AD app with a certificate, see [Use Azure PowerShell to create a service principal to access resources](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) or [Use Azure CLI to create a service principal to access resources](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).</span></span>

## <a name="get-tenant-id-from-subscription-id"></a><span data-ttu-id="eebc1-154">從訂用帳戶識別碼取得租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-154">Get tenant id from subscription id</span></span>
<span data-ttu-id="eebc1-155">若要要求可用來呼叫 Resource Manager 的權杖，應用程式必須知道裝載 Azure 訂用帳戶之 Azure AD 租用戶的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-155">To request a token that can be used to call Resource Manager, your application needs to know the tenant ID of the Azure AD tenant that hosts the Azure subscription.</span></span> <span data-ttu-id="eebc1-156">使用者很可能知道其訂用帳戶識別碼，但他們可能不知道其用於 Azure Active Directory 的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-156">Most likely, your users know their subscription ids, but they might not know their tenant ids for Azure Active Directory.</span></span> <span data-ttu-id="eebc1-157">若要取得使用者的租用戶識別碼，請要求使用者提供訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-157">To get the user's tenant id, ask the user for the subscription id.</span></span> <span data-ttu-id="eebc1-158">在傳送有關訂用帳戶的要求時，請提供該訂用帳戶識別碼：</span><span class="sxs-lookup"><span data-stu-id="eebc1-158">Provide that subscription id when sending a request about the subscription:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

<span data-ttu-id="eebc1-159">要求會因為使用者尚未登入而失敗，但您可以從回應中擷取出租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-159">The request fails because the user has not logged in yet, but you can retrieve the tenant id from the response.</span></span> <span data-ttu-id="eebc1-160">在該例外狀況中，請從 **WWW-Authenticate**的回應標頭值中擷取出租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-160">In that exception, retrieve the tenant id from the response header value for **WWW-Authenticate**.</span></span> <span data-ttu-id="eebc1-161">您可以在 [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) 方法中看到此實作。</span><span class="sxs-lookup"><span data-stu-id="eebc1-161">You see this implementation in the [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) method.</span></span>

## <a name="get-user--app-access-token"></a><span data-ttu-id="eebc1-162">取得使用者 + 應用程式的存取權杖</span><span class="sxs-lookup"><span data-stu-id="eebc1-162">Get user + app access token</span></span>
<span data-ttu-id="eebc1-163">您的應用程式會使用 OAuth 2.0 授權要求，將使用者重新導向到 Azure AD - 以驗證使用者的認證及取回授權碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-163">Your application redirects the user to Azure AD with an OAuth 2.0 Authorize Request - to authenticate the user's credentials and get back an authorization code.</span></span> <span data-ttu-id="eebc1-164">應用程式會使用授權碼來存取 Resource Manager 的權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-164">Your application uses the authorization code to get an access token for Resource Manager.</span></span> <span data-ttu-id="eebc1-165">[ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) 方法會建立授權要求。</span><span class="sxs-lookup"><span data-stu-id="eebc1-165">The [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) method creates the authorization request.</span></span>

<span data-ttu-id="eebc1-166">本主題說明用來驗證使用者的 REST API 要求。</span><span class="sxs-lookup"><span data-stu-id="eebc1-166">This topic shows the REST API requests to authenticate the user.</span></span> <span data-ttu-id="eebc1-167">您也可以使用協助程式庫以在程式碼中執行驗證。</span><span class="sxs-lookup"><span data-stu-id="eebc1-167">You can also use helper libraries to perform authentication in your code.</span></span> <span data-ttu-id="eebc1-168">如需這些程式庫的詳細資訊，請參閱 [Azure Active Directory 驗證程式庫](../active-directory/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-168">For more information about these libraries, see [Azure Active Directory Authentication Libraries](../active-directory/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="eebc1-169">如需在應用程式中整合身分識別管理的指引，請參閱 [Azure Active Directory 開發人員指南](../active-directory/active-directory-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-169">For guidance on integrating identity management in an application, see [Azure Active Directory developer's guide](../active-directory/active-directory-developers-guide.md).</span></span>

### <a name="auth-request-oauth-20"></a><span data-ttu-id="eebc1-170">驗證要求 (OAuth 2.0)</span><span class="sxs-lookup"><span data-stu-id="eebc1-170">Auth request (OAuth 2.0)</span></span>
<span data-ttu-id="eebc1-171">將開啟識別碼連線/OAuth2.0 授權要求發給 Azure AD 授權端點︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-171">Issue an Open ID Connect/OAuth2.0 Authorize Request to the Azure AD Authorize endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

<span data-ttu-id="eebc1-172">[要求授權碼](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code)主題說明適用於此要求的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="eebc1-172">The query string parameters that are available for this request are described in the [request an authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) topic.</span></span>

<span data-ttu-id="eebc1-173">下列範例示範如何要求 OAuth2.0 授權︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-173">The following example shows how to request OAuth2.0 authorization:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

<span data-ttu-id="eebc1-174">Azure AD 驗證使用者，並在需要時要求使用者將權限授與應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-174">Azure AD authenticates the user, and, if necessary, asks the user to grant permission to the app.</span></span> <span data-ttu-id="eebc1-175">它會將授權碼傳回至應用程式的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="eebc1-175">It returns the authorization code to the Reply URL of your application.</span></span> <span data-ttu-id="eebc1-176">根據要求的 response_mode，Azure AD 會在查詢字串中傳回資料，或作為張貼資料。</span><span class="sxs-lookup"><span data-stu-id="eebc1-176">Depending on the requested response_mode, Azure AD either sends back the data in query string or as post data.</span></span>

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a><span data-ttu-id="eebc1-177">驗證要求 (Open ID Connect)</span><span class="sxs-lookup"><span data-stu-id="eebc1-177">Auth request (Open ID Connect)</span></span>
<span data-ttu-id="eebc1-178">如果您不只想要代表使用者存取 Azure Resource Manager，並且允許使用者使用其 Azure AD 帳戶登入您的應用程式，請發出 Open ID Connect 授權要求。</span><span class="sxs-lookup"><span data-stu-id="eebc1-178">If you not only wish to access Azure Resource Manager on behalf of the user, but also allow the user to sign in to your application using their Azure AD account, issue an Open ID Connect Authorize Request.</span></span> <span data-ttu-id="eebc1-179">使用 Open ID Connect，您的應用程式也會收到 Azure AD 的 id_token，讓應用程式用來登入使用者。</span><span class="sxs-lookup"><span data-stu-id="eebc1-179">With Open ID Connect, your application also receives an id_token from Azure AD that your app can use to sign in the user.</span></span>

<span data-ttu-id="eebc1-180">[傳送登入要求](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request)主題說明適用於此要求的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="eebc1-180">The query string parameters that are available for this request are described in the [Send the sign-in request](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) topic.</span></span>

<span data-ttu-id="eebc1-181">Open ID Connect 的要求範例是︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-181">An example Open ID Connect request is:</span></span>

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

<span data-ttu-id="eebc1-182">Azure AD 驗證使用者，並在需要時要求使用者將權限授與應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-182">Azure AD authenticates the user, and, if necessary, asks the user to grant permission to the app.</span></span> <span data-ttu-id="eebc1-183">它會將授權碼傳回至應用程式的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="eebc1-183">It returns the authorization code to the Reply URL of your application.</span></span> <span data-ttu-id="eebc1-184">根據要求的 response_mode，Azure AD 會在查詢字串中傳回資料，或作為張貼資料。</span><span class="sxs-lookup"><span data-stu-id="eebc1-184">Depending on the requested response_mode, Azure AD either sends back the data in query string or as post data.</span></span>

<span data-ttu-id="eebc1-185">Open ID Connect 回應的範例是︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-185">An example Open ID Connect response is:</span></span>

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a><span data-ttu-id="eebc1-186">權杖要求 (OAuth2.0 程式碼授與流程)</span><span class="sxs-lookup"><span data-stu-id="eebc1-186">Token request (OAuth2.0 Code Grant Flow)</span></span>
<span data-ttu-id="eebc1-187">您的應用程式現在已從 Azure AD 收到授權碼，現在是取得 Azure Resource Manager 的存取權杖的時候了。</span><span class="sxs-lookup"><span data-stu-id="eebc1-187">Now that your application has received the authorization code from Azure AD, it is time to get the access token for Azure Resource Manager.</span></span>  <span data-ttu-id="eebc1-188">將 OAuth2.0 程式碼授與權杖要求張貼至 Azure AD 權杖端點︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-188">Post an OAuth2.0 Code Grant Token Request to the Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="eebc1-189">[使用授權碼](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token)主題說明適用於此要求的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="eebc1-189">The query string parameters that are available for this request are described in the [use the authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) topic.</span></span>

<span data-ttu-id="eebc1-190">下列範例顯示如何使用密碼認證來要求程式碼授與權杖：</span><span class="sxs-lookup"><span data-stu-id="eebc1-190">The following example shows a request for code grant token with password credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="eebc1-191">使用憑證認證時，使用您的應用程式的憑證認證的私密金鑰來建立 JSON Web 權杖 (JWT) 和登入 (RSA SHA256)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-191">When working with certificate credentials, create a JSON Web Token (JWT) and sign (RSA SHA256) using the private key of your application's certificate credential.</span></span> <span data-ttu-id="eebc1-192">[JWT 權杖宣告](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims)會說明權杖的宣告類型。</span><span class="sxs-lookup"><span data-stu-id="eebc1-192">The claim types for the token are shown in [JWT token claims](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims).</span></span> <span data-ttu-id="eebc1-193">如需參考，請參閱 [Active Directory 驗證程式庫 (.NET) 程式碼](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) 來簽署用戶端判斷提示 JWT 權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-193">For reference, see the [Active Directory Auth Library (.NET) code](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) to sign Client Assertion JWT tokens.</span></span>

<span data-ttu-id="eebc1-194">請參閱 [Open ID Connect 規格](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) 來取得用戶端驗證的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="eebc1-194">See the [Open ID Connect spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) for details on client authentication.</span></span>

<span data-ttu-id="eebc1-195">下列範例顯示如何使用憑證認證來要求程式碼授與權杖：</span><span class="sxs-lookup"><span data-stu-id="eebc1-195">The following example shows a request for code grant token with certificate credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

<span data-ttu-id="eebc1-196">程式碼授與權杖回應的範例︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-196">An example response for code grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a><span data-ttu-id="eebc1-197">處理程式碼授與權杖回應</span><span class="sxs-lookup"><span data-stu-id="eebc1-197">Handle code grant token response</span></span>
<span data-ttu-id="eebc1-198">成功的權杖回應會包含 Azure Resource Manager 的 (使用者 + 應用程式) 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-198">A successful token response contains the (user + app) access token for Azure Resource Manager.</span></span> <span data-ttu-id="eebc1-199">應用程式會使用此存取權杖來代表使用者存取 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="eebc1-199">Your application uses this access token to access Resource Manager on behalf of the user.</span></span> <span data-ttu-id="eebc1-200">Azure AD 所發出的存取權杖存留期是一小時。</span><span class="sxs-lookup"><span data-stu-id="eebc1-200">The lifetime of access tokens issued by Azure AD is one hour.</span></span> <span data-ttu-id="eebc1-201">Web 應用程式不太可能需要更新 (使用者 + 應用程式) 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-201">It is unlikely that your web application needs to renew the (user + app) access token.</span></span> <span data-ttu-id="eebc1-202">如果需要更新存取權杖，請使用應用程式在權杖回應中收到的重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-202">If it needs to renew the access token, use the refresh token that your application receives in the token response.</span></span> <span data-ttu-id="eebc1-203">將 OAuth2.0 權杖要求張貼至 Azure AD 權杖端點︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-203">Post an OAuth2.0 Token Request to the Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="eebc1-204">[重新整理存取權杖](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens)中會說明要與重新整理要求搭配使用的參數。</span><span class="sxs-lookup"><span data-stu-id="eebc1-204">The parameters to use with the refresh request are described in [refreshing the access token](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).</span></span>

<span data-ttu-id="eebc1-205">下列範例顯示如何使用重新整理權杖：</span><span class="sxs-lookup"><span data-stu-id="eebc1-205">The following example shows how to use the refresh token:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="eebc1-206">雖然重新整理權杖可用來取得 Azure Resource Manager 的新存取權杖，但它們並不適合您的應用程式離線存取。</span><span class="sxs-lookup"><span data-stu-id="eebc1-206">Although refresh tokens can be used to get new access tokens for Azure Resource Manager, they are not suitable for offline access by your application.</span></span> <span data-ttu-id="eebc1-207">重新整理權杖存留期有限，且重新整理權杖會繫結至使用者。</span><span class="sxs-lookup"><span data-stu-id="eebc1-207">The refresh tokens lifetime is limited, and refresh tokens are bound to the user.</span></span> <span data-ttu-id="eebc1-208">如果使用者離開組織，使用重新整理權杖的應用程式會無法存取。</span><span class="sxs-lookup"><span data-stu-id="eebc1-208">If the user leaves the organization, the application using the refresh token loses access.</span></span> <span data-ttu-id="eebc1-209">這個方法不適合小組用來管理其 Azure 資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-209">This approach isn't suitable for applications that are used by teams to manage their Azure resources.</span></span>

## <a name="check-if-user-can-assign-access-to-subscription"></a><span data-ttu-id="eebc1-210">檢查使用者是否可以指派訂用帳戶的存取權</span><span class="sxs-lookup"><span data-stu-id="eebc1-210">Check if user can assign access to subscription</span></span>
<span data-ttu-id="eebc1-211">您的應用程式現在具有權杖，可代表使用者存取 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="eebc1-211">Your application now has a token to access Azure Resource Manager on behalf of the user.</span></span> <span data-ttu-id="eebc1-212">下一步是將應用程式連接到訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-212">The next step is to connect your app to the subscription.</span></span> <span data-ttu-id="eebc1-213">在連接之後，即使使用者不存在 (長期離線存取)，您仍然可以管理這些訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-213">After connecting, your app can manage those subscriptions even when the user isn't present (long-term offline access).</span></span>

<span data-ttu-id="eebc1-214">針對每個要連接的訂用帳戶，請呼叫 [Resource Manager 列出權限](https://docs.microsoft.com/rest/api/authorization/permissions) API 來判斷使用者是否具有訂用帳戶的存取管理權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-214">For each subscription to connect, call the [Resource Manager list permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API to determine whether the user has access management rights for the subscription.</span></span>

<span data-ttu-id="eebc1-215">ASP.NET MVC 範例應用程式的 [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) 方法會實作這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="eebc1-215">The [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) method of the ASP.NET MVC sample app implements this call.</span></span>

<span data-ttu-id="eebc1-216">下列範例示範如何要求使用者在訂用帳戶上的權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-216">The following example shows how to request a user's permissions on a subscription.</span></span> <span data-ttu-id="eebc1-217">83cfe939-2402-4581-b761-4f59b0a041e4 是訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-217">83cfe939-2402-4581-b761-4f59b0a041e4 is the id of the subscription.</span></span>

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

<span data-ttu-id="eebc1-218">以下是針對取得使用者在訂用帳戶上的權限所做的回應範例︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-218">An example of the response to get user's permissions on subscription is:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

<span data-ttu-id="eebc1-219">權限 API 會傳回多個權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-219">The permissions API returns multiple permissions.</span></span> <span data-ttu-id="eebc1-220">每個權限包含允許的動作 (actions) 和不允許的動作 (notactions)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-220">Each permission consists of allowed actions (actions) and disallowed actions (notactions).</span></span> <span data-ttu-id="eebc1-221">如果動作出現在任何權限的允許 actions 清單中，而且不存在於該權限的 notactions 清單，則使用者可執行該動作。</span><span class="sxs-lookup"><span data-stu-id="eebc1-221">If an action is present in the allowed actions list of any permission and not present in the notactions list of that permission, the user is allowed to perform that action.</span></span> <span data-ttu-id="eebc1-222">**microsoft.authorization/roleassignments/write** 是授與存取管理權限的動作。</span><span class="sxs-lookup"><span data-stu-id="eebc1-222">**microsoft.authorization/roleassignments/write** is the action that that grants access management rights.</span></span> <span data-ttu-id="eebc1-223">您的應用程式必須剖析權限結果，才能在每個權限的 actions 和 notactions 中的此動作字串上，尋找 regex 相符項。</span><span class="sxs-lookup"><span data-stu-id="eebc1-223">Your application must parse the permissions result to look for a regex match on this action string in the actions and notactions of each permission.</span></span>

## <a name="get-app-only-access-token"></a><span data-ttu-id="eebc1-224">取得僅限應用程式存取權杖</span><span class="sxs-lookup"><span data-stu-id="eebc1-224">Get app-only access token</span></span>
<span data-ttu-id="eebc1-225">現在，您已知道使用者是否可以指派 Azure 訂用帳戶的存取權。</span><span class="sxs-lookup"><span data-stu-id="eebc1-225">Now, you know if the user can assign access to the Azure subscription.</span></span> <span data-ttu-id="eebc1-226">後續步驟如下︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-226">The next steps are:</span></span>

1. <span data-ttu-id="eebc1-227">將適當的 RBAC 角色指派給您的應用程式在訂用帳戶上的身分識別。</span><span class="sxs-lookup"><span data-stu-id="eebc1-227">Assign the appropriate RBAC role to your application's identity on the subscription.</span></span>
2. <span data-ttu-id="eebc1-228">查詢訂用帳戶上的應用程式權限，或使用僅限應用程式權杖來存取 Resource Manager，藉此驗證存取指派。</span><span class="sxs-lookup"><span data-stu-id="eebc1-228">Validate the access assignment by querying for the Application's permission on the subscription or by accessing Resource Manager using app-only token.</span></span>
3. <span data-ttu-id="eebc1-229">記錄應用程式「已連線的訂用帳戶」資料結構中的連線 - 保存訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-229">Record the connection in your applications "connected subscriptions" data structure - persisting the id of the subscription.</span></span>

<span data-ttu-id="eebc1-230">讓我們更仔細地檢視第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="eebc1-230">Let's look closer at the first step.</span></span> <span data-ttu-id="eebc1-231">若要將適當的 RBAC 角色指派給應用程式身分識別，您必須判斷︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-231">To assign the appropriate RBAC role to the application's identity, you must determine:</span></span>

* <span data-ttu-id="eebc1-232">您在使用者的 Azure Active Directory 中的應用程式身分識別的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-232">The object id of your application's identity in the user's Azure Active Directory</span></span>
* <span data-ttu-id="eebc1-233">您的應用程式在訂用帳戶上需要的 RBAC 角色的識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-233">The identifier of the RBAC role that your application requires on the subscription</span></span>

<span data-ttu-id="eebc1-234">當您的應用程式驗證來自 Azure AD 的使用者時，它會在該 Azure AD 中建立應用程式的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="eebc1-234">When your application authenticates a user from an Azure AD, it creates a service principal object for your application in that Azure AD.</span></span> <span data-ttu-id="eebc1-235">Azure 允許將 RBAC 角色指派給服務主體，以便將直接存取權授與 Azure 資源上的對應應用程式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-235">Azure allows RBAC roles to be assigned to service principals to grant direct access to corresponding applications on Azure resources.</span></span> <span data-ttu-id="eebc1-236">這就是我們想要做的確切動作。</span><span class="sxs-lookup"><span data-stu-id="eebc1-236">This action is exactly what we wish to do.</span></span> <span data-ttu-id="eebc1-237">查詢 Azure AD 圖形 API，判斷應用程式在登入使用者的 Azure AD 中的服務主體識別項。</span><span class="sxs-lookup"><span data-stu-id="eebc1-237">Query the Azure AD Graph API to determine the identifier of the service principal of your application in the signed-in user's Azure AD.</span></span>

<span data-ttu-id="eebc1-238">您只有 Azure Resource Manager 的存取權杖 - 您需要新的存取權杖以呼叫 Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="eebc1-238">You only have an access token for Azure Resource Manager - you need a new access token to call the Azure AD Graph API.</span></span> <span data-ttu-id="eebc1-239">Azure AD 中的每個應用程式都有權查詢其本身的服務主體物件，因此僅限應用程式存取權杖就已足夠。</span><span class="sxs-lookup"><span data-stu-id="eebc1-239">Every application in Azure AD has permission to query its own service principal object, so an app-only access token is sufficient.</span></span>

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a><span data-ttu-id="eebc1-240">取得 Azure AD Graph API 的僅限應用程式存取權杖</span><span class="sxs-lookup"><span data-stu-id="eebc1-240">Get app-only access token for Azure AD Graph API</span></span>
<span data-ttu-id="eebc1-241">若要驗證您的應用程式，並取得 Azure AD Graph API 的權杖，請向 Azure AD 權杖端點發出用戶端認證授與 OAuth2.0 流程權杖要求 (**http://login.microsoftonline.com/{directory_domain_name}/OAuth2/Token**)。</span><span class="sxs-lookup"><span data-stu-id="eebc1-241">To authenticate your app and get a token to Azure AD Graph API, issue a Client Credential Grant OAuth2.0 flow token request to Azure AD token endpoint (**https://login.microsoftonline.com/{directory_domain_name}/OAuth2/Token**).</span></span>

<span data-ttu-id="eebc1-242">ASP.net MVC 範例應用程式的 [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) 方法使用 Active Directory Authentication Library for .NET，以取得 Graph API 的僅限應用程式存取權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-242">The [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) method of the ASP.net MVC sample application gets an app-only access token for Graph API using the Active Directory Authentication Library for .NET.</span></span>

<span data-ttu-id="eebc1-243">[要求存取權杖](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token)主題說明適用於此要求的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="eebc1-243">The query string parameters that are available for this request are described in the [Request an Access Token](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) topic.</span></span>

<span data-ttu-id="eebc1-244">用戶端認證授與權杖要求範例︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-244">An example request for client credential grant token:</span></span>

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

<span data-ttu-id="eebc1-245">用戶端認證授與權杖回應範例︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-245">An example response for client credential grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a><span data-ttu-id="eebc1-246">取得使用者 Azure AD 中的應用程式服務主體的 ObjectId</span><span class="sxs-lookup"><span data-stu-id="eebc1-246">Get ObjectId of application service principal in user Azure AD</span></span>
<span data-ttu-id="eebc1-247">現在，使用僅限應用程式存取權杖來查詢 [Azure AD Graph 服務主體](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API，以判斷目錄中應用程式的服務主體的物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-247">Now, use the app-only access token to query the [Azure AD Graph Service Principals](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API to determine the Object Id of the application's service principal in the directory.</span></span>

<span data-ttu-id="eebc1-248">ASP.net MVC 範例應用程式的 [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) 方法會實作這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="eebc1-248">The [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) method of the ASP.net MVC sample application implements this call.</span></span>

<span data-ttu-id="eebc1-249">下列範例示範如何要求應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="eebc1-249">The following example shows how to request an application's service principal.</span></span> <span data-ttu-id="eebc1-250">a0448380-c346-4f9f-b897-c18733de9394 是應用程式的用戶端識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-250">a0448380-c346-4f9f-b897-c18733de9394 is the client id of the application.</span></span>

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

<span data-ttu-id="eebc1-251">下列範例顯示應用程式的服務主體要求的回應</span><span class="sxs-lookup"><span data-stu-id="eebc1-251">The following example shows a response to the request for an application's service principal</span></span>

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow the application to access CloudSense on behalf of the signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow the application to access CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a><span data-ttu-id="eebc1-252">取得 Azure RBAC 角色識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-252">Get Azure RBAC role identifier</span></span>
<span data-ttu-id="eebc1-253">若要將適當的 RBAC 角色指派給服務主體，您必須判斷 Azure RBAC 角色的識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-253">To assign the appropriate RBAC role to your service principal, you must determine the identifier of the Azure RBAC role.</span></span>

<span data-ttu-id="eebc1-254">您的應用程式的正確 RBAC 角色︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-254">The right RBAC role for your application:</span></span>

* <span data-ttu-id="eebc1-255">如果您的應用程式只會監視訂用帳戶而不進行任何變更，它只需要訂用帳戶上的讀取器權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-255">If your application only monitors the subscription, without making any changes, it requires only reader permissions on the subscription.</span></span> <span data-ttu-id="eebc1-256">指派 **讀取器** 角色。</span><span class="sxs-lookup"><span data-stu-id="eebc1-256">Assign the **Reader** role.</span></span>
* <span data-ttu-id="eebc1-257">如果您的應用程式管理 Azure 訂用帳戶，建立/修改/刪除實體，它需要其中一個參與者權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-257">If your application manages Azure the subscription, creating/modifying/deleting entities, it requires one of the contributor permissions.</span></span>
  * <span data-ttu-id="eebc1-258">若要管理特定類型的資源，請指派資源的特定參與者角色 (虛擬機器參與者、虛擬網路參與者、儲存體帳戶參與者等)</span><span class="sxs-lookup"><span data-stu-id="eebc1-258">To manage a particular type of resource, assign the resource-specific contributor roles (Virtual Machine Contributor, Virtual Network Contributor, Storage Account Contributor, etc.)</span></span>
  * <span data-ttu-id="eebc1-259">若要管理任何資源類型，請指派 **參與者** 角色。</span><span class="sxs-lookup"><span data-stu-id="eebc1-259">To manage any resource type, assign the **Contributor** role.</span></span>

<span data-ttu-id="eebc1-260">您應用程式的角色指派會對使用者顯示，因此請選取必要的最低權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-260">The role assignment for your application is visible to users, so select the least-required privilege.</span></span>

<span data-ttu-id="eebc1-261">呼叫 [Resource Manager 角色定義 API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) 來列出所有 Azure RBAC 角色和搜尋，然後逐一查看結果，按名稱尋找所需的角色定義。</span><span class="sxs-lookup"><span data-stu-id="eebc1-261">Call the [Resource Manager role definition API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) to list all Azure RBAC roles and search then iterate over the result to find the desired role definition by name.</span></span>

<span data-ttu-id="eebc1-262">ASP.net MVC 範例應用程式的 [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) 方法會實作這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="eebc1-262">The [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) method of the ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="eebc1-263">下列要求範例示範如何取得 Azure RBAC 角色識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-263">The following request example shows how to get Azure RBAC role identifier.</span></span> <span data-ttu-id="eebc1-264">09cbd307-aa71-4aca-b346-5f253e6e3ebb 是訂用帳戶的識別碼。</span><span class="sxs-lookup"><span data-stu-id="eebc1-264">09cbd307-aa71-4aca-b346-5f253e6e3ebb is the id of the subscription.</span></span>

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

<span data-ttu-id="eebc1-265">回應格式如下：</span><span class="sxs-lookup"><span data-stu-id="eebc1-265">The response is in the following format:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access to them.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access to them.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

<span data-ttu-id="eebc1-266">您不需要持續呼叫此 API。</span><span class="sxs-lookup"><span data-stu-id="eebc1-266">You do not need to call this API on an ongoing basis.</span></span> <span data-ttu-id="eebc1-267">一旦決定角色定義的已知 GUID，您可以將角色定義識別碼建構為︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-267">Once you've determined the well-known GUID of the role definition, you can construct the role definition id as:</span></span>

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

<span data-ttu-id="eebc1-268">以下是常用的內建角色的知名 guid：</span><span class="sxs-lookup"><span data-stu-id="eebc1-268">Here are the well-known guids of commonly used built-in roles:</span></span>

| <span data-ttu-id="eebc1-269">角色</span><span class="sxs-lookup"><span data-stu-id="eebc1-269">Role</span></span> | <span data-ttu-id="eebc1-270">Guid</span><span class="sxs-lookup"><span data-stu-id="eebc1-270">Guid</span></span> |
| --- | --- |
| <span data-ttu-id="eebc1-271">讀取器</span><span class="sxs-lookup"><span data-stu-id="eebc1-271">Reader</span></span> |<span data-ttu-id="eebc1-272">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="eebc1-272">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |
| <span data-ttu-id="eebc1-273">參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-273">Contributor</span></span> |<span data-ttu-id="eebc1-274">b24988ac-6180-42a0-ab88-20f7382dd24c</span><span class="sxs-lookup"><span data-stu-id="eebc1-274">b24988ac-6180-42a0-ab88-20f7382dd24c</span></span> |
| <span data-ttu-id="eebc1-275">虛擬機器參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-275">Virtual Machine Contributor</span></span> |<span data-ttu-id="eebc1-276">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span><span class="sxs-lookup"><span data-stu-id="eebc1-276">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span></span> |
| <span data-ttu-id="eebc1-277">虛擬網路參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-277">Virtual Network Contributor</span></span> |<span data-ttu-id="eebc1-278">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span><span class="sxs-lookup"><span data-stu-id="eebc1-278">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span></span> |
| <span data-ttu-id="eebc1-279">儲存體帳戶參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-279">Storage Account Contributor</span></span> |<span data-ttu-id="eebc1-280">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span><span class="sxs-lookup"><span data-stu-id="eebc1-280">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span></span> |
| <span data-ttu-id="eebc1-281">網站參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-281">Website Contributor</span></span> |<span data-ttu-id="eebc1-282">de139f84-1756-47ae-9be6-808fbbe84772</span><span class="sxs-lookup"><span data-stu-id="eebc1-282">de139f84-1756-47ae-9be6-808fbbe84772</span></span> |
| <span data-ttu-id="eebc1-283">Web 方案參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-283">Web Plan Contributor</span></span> |<span data-ttu-id="eebc1-284">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span><span class="sxs-lookup"><span data-stu-id="eebc1-284">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span></span> |
| <span data-ttu-id="eebc1-285">SQL Server 參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-285">SQL Server Contributor</span></span> |<span data-ttu-id="eebc1-286">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span><span class="sxs-lookup"><span data-stu-id="eebc1-286">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span></span> |
| <span data-ttu-id="eebc1-287">SQL DB 參與者</span><span class="sxs-lookup"><span data-stu-id="eebc1-287">SQL DB Contributor</span></span> |<span data-ttu-id="eebc1-288">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span><span class="sxs-lookup"><span data-stu-id="eebc1-288">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span></span> |

### <a name="assign-rbac-role-to-application"></a><span data-ttu-id="eebc1-289">將 RBAC 角色指派給應用程式</span><span class="sxs-lookup"><span data-stu-id="eebc1-289">Assign RBAC role to application</span></span>
<span data-ttu-id="eebc1-290">您已具備所有條件，可使用 [Resource Manager 建立角色指派](https://docs.microsoft.com/rest/api/authorization/roleassignments) API，將適當的 RBAC 角色指派給服務主體。</span><span class="sxs-lookup"><span data-stu-id="eebc1-290">You have everything you need to assign the appropriate RBAC role to your service principal by using the [Resource Manager create role assignment](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.</span></span>

<span data-ttu-id="eebc1-291">ASP.net MVC 範例應用程式的 [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) 方法會實作這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="eebc1-291">The [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) method of the ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="eebc1-292">將 RBAC 角色指派給應用程式的要求範例︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-292">An example request to assign RBAC role to application:</span></span>

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

<span data-ttu-id="eebc1-293">在要求中，使用下列值︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-293">In the request, the following values are used:</span></span>

| <span data-ttu-id="eebc1-294">Guid</span><span class="sxs-lookup"><span data-stu-id="eebc1-294">Guid</span></span> | <span data-ttu-id="eebc1-295">說明</span><span class="sxs-lookup"><span data-stu-id="eebc1-295">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eebc1-296">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span><span class="sxs-lookup"><span data-stu-id="eebc1-296">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span></span> |<span data-ttu-id="eebc1-297">訂用帳戶的識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-297">the id of the subscription</span></span> |
| <span data-ttu-id="eebc1-298">c3097b31-7309-4c59-b4e3-770f8406bad2</span><span class="sxs-lookup"><span data-stu-id="eebc1-298">c3097b31-7309-4c59-b4e3-770f8406bad2</span></span> |<span data-ttu-id="eebc1-299">應用程式的服務主體的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-299">the object id of the service principal of the application</span></span> |
| <span data-ttu-id="eebc1-300">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="eebc1-300">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |<span data-ttu-id="eebc1-301">讀取器角色的識別碼</span><span class="sxs-lookup"><span data-stu-id="eebc1-301">the id of the reader role</span></span> |
| <span data-ttu-id="eebc1-302">4f87261d-2816-465d-8311-70a27558df4c</span><span class="sxs-lookup"><span data-stu-id="eebc1-302">4f87261d-2816-465d-8311-70a27558df4c</span></span> |<span data-ttu-id="eebc1-303">為新角色指派建立的新 guid</span><span class="sxs-lookup"><span data-stu-id="eebc1-303">a new guid created for the new role assignment</span></span> |

<span data-ttu-id="eebc1-304">回應格式如下：</span><span class="sxs-lookup"><span data-stu-id="eebc1-304">The response is in the following format:</span></span>

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a><span data-ttu-id="eebc1-305">取得 Azure Resource Manager 的僅限應用程式存取權杖</span><span class="sxs-lookup"><span data-stu-id="eebc1-305">Get app-only access token for Azure Resource Manager</span></span>
<span data-ttu-id="eebc1-306">若要驗證應用程式具有所需的訂用帳戶存取權，請使用僅限應用程式權杖對訂用帳戶執行測試工作。</span><span class="sxs-lookup"><span data-stu-id="eebc1-306">To validate that app has the desired access on the subscription, perform a test task on the subscription using an app-only token.</span></span>

<span data-ttu-id="eebc1-307">若要取得僅限應用程式存取權杖，請依照 [取得 Azure AD Graph API 的僅限應用程式存取權杖](#app-azure-ad-graph)一節的指示，為資源參數使用不同值︰</span><span class="sxs-lookup"><span data-stu-id="eebc1-307">To get an app-only access token, follow instructions from section [Get app-only access token for Azure AD Graph API](#app-azure-ad-graph), with a different value for the resource parameter:</span></span>

    https://management.core.windows.net/

<span data-ttu-id="eebc1-308">ASP.NET MVC 範例應用程式的 [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) 方法使用 Active Directory Authentication Library for .net，以取得 Azure Resource Manager 的僅限應用程式存取權杖。</span><span class="sxs-lookup"><span data-stu-id="eebc1-308">The [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of the ASP.NET MVC sample application gets an app-only access token for Azure Resource Manager using the Active Directory Authentication Library for .net.</span></span>

#### <a name="get-applications-permissions-on-subscription"></a><span data-ttu-id="eebc1-309">取得訂用帳戶上的應用程式權限</span><span class="sxs-lookup"><span data-stu-id="eebc1-309">Get Application's Permissions on Subscription</span></span>
<span data-ttu-id="eebc1-310">若要檢查應用程式是否具有 Azure 訂用帳戶上的所需存取權，您也可以呼叫 [Resource Manager 權限](https://docs.microsoft.com/rest/api/authorization/permissions) API。</span><span class="sxs-lookup"><span data-stu-id="eebc1-310">To check that your application has the desired access on an Azure subscription, you may also call the [Resource Manager Permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API.</span></span> <span data-ttu-id="eebc1-311">此方式類似於您用來判斷使用者是否具有訂用帳戶存取管理權限的方式。</span><span class="sxs-lookup"><span data-stu-id="eebc1-311">This approach is similar to how you determined whether the user has Access Management rights for the subscription.</span></span> <span data-ttu-id="eebc1-312">不過，此時會使用您在上一個步驟中收到的僅限應用程式存取權杖來呼叫 API 權限。</span><span class="sxs-lookup"><span data-stu-id="eebc1-312">However, this time, call the permissions API with the app-only access token that you received in the previous step.</span></span>

<span data-ttu-id="eebc1-313">ASP.NET MVC 範例應用程式的 [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) 方法會實作這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="eebc1-313">The [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of the ASP.NET MVC sample app implements this call.</span></span>

## <a name="manage-connected-subscriptions"></a><span data-ttu-id="eebc1-314">管理連接的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="eebc1-314">Manage connected subscriptions</span></span>
<span data-ttu-id="eebc1-315">將適當的 RBAC 角色指派給應用程式在訂用帳戶上的服務主體時，您的應用程式可使用 Azure Resource Manager 的僅限應用程式存取權杖以持續監視/管理它。</span><span class="sxs-lookup"><span data-stu-id="eebc1-315">When the appropriate RBAC role is assigned to your application's service principal on the subscription, your application can keep monitoring/managing it using app-only access tokens for Azure Resource Manager.</span></span>

<span data-ttu-id="eebc1-316">如果訂用帳戶擁有者使用傳統入口網站或命令列工具來移除應用程式的角色指派，您的應用程式便無法再存取該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-316">If a subscription owner removes your application's role assignment using the classic portal or command-line tools, your application is no longer able to access that subscription.</span></span> <span data-ttu-id="eebc1-317">在此情況下，您應該通知使用者：應用程式外部的訂用帳戶連線已中斷，然後提供他們 [修復] 連線的選項。</span><span class="sxs-lookup"><span data-stu-id="eebc1-317">In that case, you should notify the user that the connection with the subscription was severed from outside the application and give them an option to "repair" the connection.</span></span> <span data-ttu-id="eebc1-318">[修復] 只會重新建立離線刪除的角色指派。</span><span class="sxs-lookup"><span data-stu-id="eebc1-318">"Repair" would simply re-create the role assignment that was deleted offline.</span></span>

<span data-ttu-id="eebc1-319">就像您讓使用者將訂用帳戶連接到您的應用程式，您也必須允許使用者中斷連線訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-319">Just as you enabled the user to connect subscriptions to your application, you must allow the user to disconnect subscriptions too.</span></span> <span data-ttu-id="eebc1-320">從存取管理的觀點而言，中斷連線意味移除應用程式的服務主體已在訂用帳戶上的角色指派。</span><span class="sxs-lookup"><span data-stu-id="eebc1-320">From an access management point of view, disconnect means removing the role assignment that the application's service principal has on the subscription.</span></span> <span data-ttu-id="eebc1-321">(選擇性) 也可能移除訂用帳戶的應用程式中的任何狀態。</span><span class="sxs-lookup"><span data-stu-id="eebc1-321">Optionally, any state in the application for the subscription might be removed too.</span></span>
<span data-ttu-id="eebc1-322">只有在訂用帳戶上具有存取管理權限的使用者能夠中斷連線訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-322">Only users with access management permission on the subscription are able to disconnect the subscription.</span></span>

<span data-ttu-id="eebc1-323">ASP.net MVC 範例應用程式的 [RevokeRoleFromServicePrincipalOnSubscription 方法](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) 會實作這個呼叫。</span><span class="sxs-lookup"><span data-stu-id="eebc1-323">The [RevokeRoleFromServicePrincipalOnSubscription method](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) of the ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="eebc1-324">大功告成，使用者現在能使用您的應用程式來輕鬆連接及管理其 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="eebc1-324">That's it - users can now easily connect and manage their Azure subscriptions with your application.</span></span>
