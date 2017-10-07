---
title: "aaaAzure Active Directory 驗證和資源管理員 |Microsoft 文件"
description: "開發人員指南 tooauthentication hello Azure 資源管理員 API 和 Azure Active Directory 整合應用程式與其他 Azure 訂用帳戶。"
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
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a><span data-ttu-id="1b31e-103">使用資源管理員 API 驗證 tooaccess 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b31e-103">Use Resource Manager authentication API tooaccess subscriptions</span></span>
## <a name="introduction"></a><span data-ttu-id="1b31e-104">簡介</span><span class="sxs-lookup"><span data-stu-id="1b31e-104">Introduction</span></span>
<span data-ttu-id="1b31e-105">如果您是軟體開發人員需要 toocreate 管理客戶的 Azure 資源的應用程式，本主題，說明如何使用 tooauthenticate hello Azure 資源管理員 Api，並取得存取 tooresources 其他訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="1b31e-105">If you are a software developer who needs toocreate an app that manages customer's Azure resources, this topic shows you how tooauthenticate with hello Azure Resource Manager APIs and gain access tooresources in other subscriptions.</span></span>

<span data-ttu-id="1b31e-106">您的應用程式可以存取數種方式中的資源管理員 Api hello:</span><span class="sxs-lookup"><span data-stu-id="1b31e-106">Your app can access hello Resource Manager APIs in couple of ways:</span></span>

1. <span data-ttu-id="1b31e-107">**使用者 + 應用程式存取**︰適用於代表登入使用者存取資源的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-107">**User + app access**: for apps that access resources on behalf of a signed-in user.</span></span> <span data-ttu-id="1b31e-108">此方式適用於僅處理「互動式管理」Azure 資源的應用程式，例如 Web 應用程式和命令列工具。</span><span class="sxs-lookup"><span data-stu-id="1b31e-108">This approach works for apps, such as web apps and command-line tools, that deal with only "interactive management" of Azure resources.</span></span>
2. <span data-ttu-id="1b31e-109">**僅限應用程式存取**︰適用於執行協助程式服務和已排程之作業的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-109">**App-only access**: for apps that run daemon services and scheduled jobs.</span></span> <span data-ttu-id="1b31e-110">hello 應用程式的身分識別會授與直接存取 toohello 資源。</span><span class="sxs-lookup"><span data-stu-id="1b31e-110">hello app's identity is granted direct access toohello resources.</span></span> <span data-ttu-id="1b31e-111">這個方法適用於需要長期的遠端控制 （自動） 存取 tooAzure 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-111">This approach works for apps that need long-term headless (unattended) access tooAzure.</span></span>

<span data-ttu-id="1b31e-112">本主題提供逐步指示 toocreate 採用這兩種授權方法的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-112">This topic provides step-by-step instructions toocreate an app that employs both these authorization methods.</span></span> <span data-ttu-id="1b31e-113">它會顯示如何 tooperform 每個步驟來搭配 REST API 或 C#。</span><span class="sxs-lookup"><span data-stu-id="1b31e-113">It shows how tooperform each step with REST API or C#.</span></span> <span data-ttu-id="1b31e-114">hello 完整的 ASP.NET MVC 應用程式將會位於[https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-114">hello complete ASP.NET MVC application is available at [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).</span></span>

## <a name="what-hello-web-app-does"></a><span data-ttu-id="1b31e-115">沒有什麼 hello web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1b31e-115">What hello web app does</span></span>
<span data-ttu-id="1b31e-116">hello web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="1b31e-116">hello web app:</span></span>

1. <span data-ttu-id="1b31e-117">登入 Azure 使用者。</span><span class="sxs-lookup"><span data-stu-id="1b31e-117">Signs-in an Azure user.</span></span>
2. <span data-ttu-id="1b31e-118">會要求使用者 toogrant hello web 應用程式存取 tooResource 管理員。</span><span class="sxs-lookup"><span data-stu-id="1b31e-118">Asks user toogrant hello web app access tooResource Manager.</span></span>
3. <span data-ttu-id="1b31e-119">取得使用者 + 應用程式的存取權杖來存取 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="1b31e-119">Gets user + app access token for accessing Resource Manager.</span></span>
4. <span data-ttu-id="1b31e-120">Hello 訂用帳戶，可讓 hello 應用程式長期存取 toohello 訂用帳戶中，會使用語彙基元 （從步驟 3） toocall 資源管理員和指派 hello 應用程式的服務主體 tooa 角色。</span><span class="sxs-lookup"><span data-stu-id="1b31e-120">Uses token (from step 3) toocall Resource Manager and assign hello app's service principal tooa role in hello subscription, which gives hello app long-term access toohello subscription.</span></span>
5. <span data-ttu-id="1b31e-121">取得僅限應用程式存取權杖。</span><span class="sxs-lookup"><span data-stu-id="1b31e-121">Gets app-only access token.</span></span>
6. <span data-ttu-id="1b31e-122">Hello 訂用帳戶透過資源管理員中，會使用語彙基元 （來自步驟 5） toomanage 資源。</span><span class="sxs-lookup"><span data-stu-id="1b31e-122">Uses token (from step 5) toomanage resources in hello subscription through Resource Manager.</span></span>

<span data-ttu-id="1b31e-123">以下是 hello hello web 應用程式的端對端流程。</span><span class="sxs-lookup"><span data-stu-id="1b31e-123">Here's hello end-to-end flow of hello web application.</span></span>

![Resource Manager 驗證流程](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

<span data-ttu-id="1b31e-125">身為使用者，您可以提供 hello 訂用帳戶 id 想 toouse hello 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="1b31e-125">As a user, you provide hello subscription id for hello subscription you want toouse:</span></span>

![提供訂用帳戶識別碼](./media/resource-manager-api-authentication/sample-ux-1.png)

<span data-ttu-id="1b31e-127">選取 hello 帳戶 toouse 進行登入。</span><span class="sxs-lookup"><span data-stu-id="1b31e-127">Select hello account toouse for logging in.</span></span>

![選取帳戶](./media/resource-manager-api-authentication/sample-ux-2.png)

<span data-ttu-id="1b31e-129">提供您的認證。</span><span class="sxs-lookup"><span data-stu-id="1b31e-129">Provide your credentials.</span></span>

![提供認證](./media/resource-manager-api-authentication/sample-ux-3.png)

<span data-ttu-id="1b31e-131">授與 hello 應用程式存取 tooyour Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="1b31e-131">Grant hello app access tooyour Azure subscriptions:</span></span>

![授與存取權](./media/resource-manager-api-authentication/sample-ux-4.png)

<span data-ttu-id="1b31e-133">管理連接的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="1b31e-133">Manage your connected subscriptions:</span></span>

![連線訂用帳戶](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a><span data-ttu-id="1b31e-135">註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="1b31e-135">Register application</span></span>
<span data-ttu-id="1b31e-136">在開始撰寫程式碼之前，請先使用 Azure Active Directory (AD) 註冊 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-136">Before you start coding, register your web app with Azure Active Directory (AD).</span></span> <span data-ttu-id="1b31e-137">hello 應用程式註冊在 Azure AD 中建立應用程式的中央識別身分。</span><span class="sxs-lookup"><span data-stu-id="1b31e-137">hello app registration creates a central identity for your app in Azure AD.</span></span> <span data-ttu-id="1b31e-138">它會保留應用程式使用 tooauthenticate 和存取 Azure 資源管理員 Api 應用程式，例如 OAuth 用戶端識別碼、 回覆 Url 和認證的相關基本資訊。</span><span class="sxs-lookup"><span data-stu-id="1b31e-138">It holds basic information about your application like OAuth Client ID, Reply URLs, and credentials that your application uses tooauthenticate and access Azure Resource Manager APIs.</span></span> <span data-ttu-id="1b31e-139">hello 應用程式登錄也會記錄的 hello 各種委派代表 hello 使用者存取 Microsoft 應用程式開發介面時，需要您的應用程式的權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-139">hello app registration also records hello various delegated permissions that your application needs when accessing Microsoft APIs on behalf of hello user.</span></span>

<span data-ttu-id="1b31e-140">由於應用程式會存取其他訂用帳戶，您必須將它設定為多租用戶應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-140">Because your app accesses other subscription, you must configure it as a multi-tenant application.</span></span> <span data-ttu-id="1b31e-141">toopass 驗證提供與 Azure Active Directory 相關聯的網域。</span><span class="sxs-lookup"><span data-stu-id="1b31e-141">toopass validation, provide a domain associated with your Azure Active Directory.</span></span> <span data-ttu-id="1b31e-142">Azure Active Directory，登入 toohello 與相關聯的 toosee hello 網域[傳統入口網站](https://manage.windowsazure.com)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-142">toosee hello domains associated with your Azure Active Directory, log in toohello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="1b31e-143">選取您的 Azure Active Directory，然後選取 [網域]。</span><span class="sxs-lookup"><span data-stu-id="1b31e-143">Select your Azure Active Directory and then select **Domains**.</span></span>

<span data-ttu-id="1b31e-144">hello 下列範例顯示如何 tooregister hello 使用 Azure PowerShell 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-144">hello following example shows how tooregister hello app by using Azure PowerShell.</span></span> <span data-ttu-id="1b31e-145">您必須擁有 hello 最新版本 (年 8 月 2016) 的 Azure PowerShell 這個命令 toowork。</span><span class="sxs-lookup"><span data-stu-id="1b31e-145">You must have hello latest version (August 2016) of Azure PowerShell for this command toowork.</span></span>

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

<span data-ttu-id="1b31e-146">toolog 中的為 hello AD 應用程式，您需要 hello 應用程式識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-146">toolog in as hello AD application, you need hello application id and password.</span></span> <span data-ttu-id="1b31e-147">傳回從 hello 前一個命令，使用 toosee hello 應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="1b31e-147">toosee hello application id that is returned from hello previous command, use:</span></span>

    $app.ApplicationId

<span data-ttu-id="1b31e-148">下列範例中的 hello 顯示 tooregister 如何使用 Azure CLI hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-148">hello following example shows how tooregister hello app by using Azure CLI.</span></span>

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

<span data-ttu-id="1b31e-149">hello 結果包含 hello hello 應用程式以進行驗證時，您需要的 AppId。</span><span class="sxs-lookup"><span data-stu-id="1b31e-149">hello results include hello AppId, which you need when authenticating as hello application.</span></span>

### <a name="optional-configuration---certificate-credential"></a><span data-ttu-id="1b31e-150">選擇性組態 - 憑證認證</span><span class="sxs-lookup"><span data-stu-id="1b31e-150">Optional configuration - certificate credential</span></span>
<span data-ttu-id="1b31e-151">Azure AD 也支援憑證認證的應用程式： 您建立自我簽署的憑證、 保留 hello 私用金鑰，以及新增 hello 公用金鑰 tooyour Azure AD 應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="1b31e-151">Azure AD also supports certificate credentials for applications: you create a self-signed cert, keep hello private key, and add hello public key tooyour Azure AD application registration.</span></span> <span data-ttu-id="1b31e-152">進行驗證，您的應用程式會傳送小裝載 tooAzure 使用您的私密金鑰來簽署 AD 與 Azure AD 會驗證使用 hello 註冊，讓您的公用金鑰 hello 簽章。</span><span class="sxs-lookup"><span data-stu-id="1b31e-152">For authentication, your application sends a small payload tooAzure AD signed using your private key, and Azure AD validates hello signature using hello public key that you registered.</span></span>

<span data-ttu-id="1b31e-153">使用憑證建立 AD 應用程式的詳細資訊，請參閱[使用 Azure PowerShell toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority)或[使用 Azure CLI toocreate 服務主體 tooaccess 資源](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).</span><span class="sxs-lookup"><span data-stu-id="1b31e-153">For information about creating an AD app with a certificate, see [Use Azure PowerShell toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) or [Use Azure CLI toocreate a service principal tooaccess resources](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).</span></span>

## <a name="get-tenant-id-from-subscription-id"></a><span data-ttu-id="1b31e-154">從訂用帳戶識別碼取得租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-154">Get tenant id from subscription id</span></span>
<span data-ttu-id="1b31e-155">toorequest 語彙基元可能是使用的 toocall 資源管理員，您的應用程式必須裝載 hello Azure 訂用帳戶的 hello Azure AD 租用戶 tooknow hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-155">toorequest a token that can be used toocall Resource Manager, your application needs tooknow hello tenant ID of hello Azure AD tenant that hosts hello Azure subscription.</span></span> <span data-ttu-id="1b31e-156">使用者很可能知道其訂用帳戶識別碼，但他們可能不知道其用於 Azure Active Directory 的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-156">Most likely, your users know their subscription ids, but they might not know their tenant ids for Azure Active Directory.</span></span> <span data-ttu-id="1b31e-157">tooget hello 使用者的租用戶識別碼，hello 使用者尋求 hello 訂用帳戶 id。傳送嗨訂用帳戶的相關要求時，請提供該訂用帳戶 id:</span><span class="sxs-lookup"><span data-stu-id="1b31e-157">tooget hello user's tenant id, ask hello user for hello subscription id. Provide that subscription id when sending a request about hello subscription:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

<span data-ttu-id="1b31e-158">hello 要求失敗是因為 hello 使用者尚未登入，但您可以擷取 hello 回應 hello 租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-158">hello request fails because hello user has not logged in yet, but you can retrieve hello tenant id from hello response.</span></span> <span data-ttu-id="1b31e-159">在該例外狀況，請從 hello 回應標頭值中擷取 hello 租用戶識別碼**Www-authenticate**。</span><span class="sxs-lookup"><span data-stu-id="1b31e-159">In that exception, retrieve hello tenant id from hello response header value for **WWW-Authenticate**.</span></span> <span data-ttu-id="1b31e-160">您會看到此實作中 hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20)方法。</span><span class="sxs-lookup"><span data-stu-id="1b31e-160">You see this implementation in hello [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) method.</span></span>

## <a name="get-user--app-access-token"></a><span data-ttu-id="1b31e-161">取得使用者 + 應用程式的存取權杖</span><span class="sxs-lookup"><span data-stu-id="1b31e-161">Get user + app access token</span></span>
<span data-ttu-id="1b31e-162">您的應用程式重新導向 hello 使用者 tooAzure AD 的 OAuth 2.0 授權要求-tooauthenticate hello 使用者的認證，並取得授權碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-162">Your application redirects hello user tooAzure AD with an OAuth 2.0 Authorize Request - tooauthenticate hello user's credentials and get back an authorization code.</span></span> <span data-ttu-id="1b31e-163">您的應用程式會使用資源管理員的 hello 授權程式碼 tooget 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="1b31e-163">Your application uses hello authorization code tooget an access token for Resource Manager.</span></span> <span data-ttu-id="1b31e-164">hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42)方法會建立 hello 授權要求。</span><span class="sxs-lookup"><span data-stu-id="1b31e-164">hello [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) method creates hello authorization request.</span></span>

<span data-ttu-id="1b31e-165">本主題顯示 hello REST API 要求 tooauthenticate hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="1b31e-165">This topic shows hello REST API requests tooauthenticate hello user.</span></span> <span data-ttu-id="1b31e-166">您也可以使用協助程式程式庫 tooperform 驗證程式碼中。</span><span class="sxs-lookup"><span data-stu-id="1b31e-166">You can also use helper libraries tooperform authentication in your code.</span></span> <span data-ttu-id="1b31e-167">如需這些程式庫的詳細資訊，請參閱 [Azure Active Directory 驗證程式庫](../active-directory/active-directory-authentication-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-167">For more information about these libraries, see [Azure Active Directory Authentication Libraries](../active-directory/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="1b31e-168">如需在應用程式中整合身分識別管理的指引，請參閱 [Azure Active Directory 開發人員指南](../active-directory/active-directory-developers-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-168">For guidance on integrating identity management in an application, see [Azure Active Directory developer's guide](../active-directory/active-directory-developers-guide.md).</span></span>

### <a name="auth-request-oauth-20"></a><span data-ttu-id="1b31e-169">驗證要求 (OAuth 2.0)</span><span class="sxs-lookup"><span data-stu-id="1b31e-169">Auth request (OAuth 2.0)</span></span>
<span data-ttu-id="1b31e-170">發出開啟識別碼連接/OAuth2.0 授權要求 toohello Azure AD 授權端點：</span><span class="sxs-lookup"><span data-stu-id="1b31e-170">Issue an Open ID Connect/OAuth2.0 Authorize Request toohello Azure AD Authorize endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

<span data-ttu-id="1b31e-171">hello 查詢字串參數可用於此要求所述 hello[要求授權碼](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code)主題。</span><span class="sxs-lookup"><span data-stu-id="1b31e-171">hello query string parameters that are available for this request are described in hello [request an authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) topic.</span></span>

<span data-ttu-id="1b31e-172">下列範例會示範如何 hello toorequest OAuth2.0 授權：</span><span class="sxs-lookup"><span data-stu-id="1b31e-172">hello following example shows how toorequest OAuth2.0 authorization:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

<span data-ttu-id="1b31e-173">Azure AD 驗證 hello 使用者，並視需要要求 hello 使用者 toogrant 權限 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-173">Azure AD authenticates hello user, and, if necessary, asks hello user toogrant permission toohello app.</span></span> <span data-ttu-id="1b31e-174">它會傳回 hello 授權程式碼 toohello 應用程式的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="1b31e-174">It returns hello authorization code toohello Reply URL of your application.</span></span> <span data-ttu-id="1b31e-175">根據 hello 要求 response_mode，任一個傳送回 hello 資料查詢字串或張貼資料的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1b31e-175">Depending on hello requested response_mode, Azure AD either sends back hello data in query string or as post data.</span></span>

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a><span data-ttu-id="1b31e-176">驗證要求 (Open ID Connect)</span><span class="sxs-lookup"><span data-stu-id="1b31e-176">Auth request (Open ID Connect)</span></span>
<span data-ttu-id="1b31e-177">如果您不只想 tooaccess Azure 資源管理員代表 hello 使用者，但也允許 hello 使用者 toosign tooyour 使用其 Azure AD 帳戶的應用程式中，發出開啟識別碼連線授權要求。</span><span class="sxs-lookup"><span data-stu-id="1b31e-177">If you not only wish tooaccess Azure Resource Manager on behalf of hello user, but also allow hello user toosign in tooyour application using their Azure AD account, issue an Open ID Connect Authorize Request.</span></span> <span data-ttu-id="1b31e-178">開啟連接識別碼，與您的應用程式也會收到 id_token 從您的應用程式，可以使用 toosign hello 使用者在 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1b31e-178">With Open ID Connect, your application also receives an id_token from Azure AD that your app can use toosign in hello user.</span></span>

<span data-ttu-id="1b31e-179">hello 查詢字串參數可用於此要求所述 hello[登入要求傳送嗨](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request)主題。</span><span class="sxs-lookup"><span data-stu-id="1b31e-179">hello query string parameters that are available for this request are described in hello [Send hello sign-in request](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) topic.</span></span>

<span data-ttu-id="1b31e-180">Open ID Connect 的要求範例是︰</span><span class="sxs-lookup"><span data-stu-id="1b31e-180">An example Open ID Connect request is:</span></span>

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

<span data-ttu-id="1b31e-181">Azure AD 驗證 hello 使用者，並視需要要求 hello 使用者 toogrant 權限 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-181">Azure AD authenticates hello user, and, if necessary, asks hello user toogrant permission toohello app.</span></span> <span data-ttu-id="1b31e-182">它會傳回 hello 授權程式碼 toohello 應用程式的回覆 URL。</span><span class="sxs-lookup"><span data-stu-id="1b31e-182">It returns hello authorization code toohello Reply URL of your application.</span></span> <span data-ttu-id="1b31e-183">根據 hello 要求 response_mode，任一個傳送回 hello 資料查詢字串或張貼資料的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1b31e-183">Depending on hello requested response_mode, Azure AD either sends back hello data in query string or as post data.</span></span>

<span data-ttu-id="1b31e-184">Open ID Connect 回應的範例是︰</span><span class="sxs-lookup"><span data-stu-id="1b31e-184">An example Open ID Connect response is:</span></span>

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a><span data-ttu-id="1b31e-185">權杖要求 (OAuth2.0 程式碼授與流程)</span><span class="sxs-lookup"><span data-stu-id="1b31e-185">Token request (OAuth2.0 Code Grant Flow)</span></span>
<span data-ttu-id="1b31e-186">現在，您的應用程式已收到來自 Azure AD 的 hello 授權碼，它會是時間 tooget hello 存取語彙基元的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1b31e-186">Now that your application has received hello authorization code from Azure AD, it is time tooget hello access token for Azure Resource Manager.</span></span>  <span data-ttu-id="1b31e-187">張貼 OAuth2.0 程式碼授與權杖要求 toohello Azure AD 權杖端點：</span><span class="sxs-lookup"><span data-stu-id="1b31e-187">Post an OAuth2.0 Code Grant Token Request toohello Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="1b31e-188">hello 查詢字串參數可用於此要求所述 hello[使用 hello 授權碼](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token)主題。</span><span class="sxs-lookup"><span data-stu-id="1b31e-188">hello query string parameters that are available for this request are described in hello [use hello authorization code](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) topic.</span></span>

<span data-ttu-id="1b31e-189">hello 下列範例顯示使用密碼認證的程式碼授與權杖的要求：</span><span class="sxs-lookup"><span data-stu-id="1b31e-189">hello following example shows a request for code grant token with password credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="1b31e-190">當使用憑證認證，建立 JSON Web Token (JWT) 並登入 (RSA SHA256) 使用的應用程式的憑證認證 hello 私密金鑰。</span><span class="sxs-lookup"><span data-stu-id="1b31e-190">When working with certificate credentials, create a JSON Web Token (JWT) and sign (RSA SHA256) using hello private key of your application's certificate credential.</span></span> <span data-ttu-id="1b31e-191">hello hello 語彙基元的宣告型別如下所示[JWT 權杖宣告](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-191">hello claim types for hello token are shown in [JWT token claims](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims).</span></span> <span data-ttu-id="1b31e-192">如需參考，請參閱 hello [Active Directory 驗證程式庫 (.NET) 程式碼](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs)toosign 用戶端判斷提示的 JWT 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="1b31e-192">For reference, see hello [Active Directory Auth Library (.NET) code](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign Client Assertion JWT tokens.</span></span>

<span data-ttu-id="1b31e-193">請參閱 hello[開啟連接的識別碼規格](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication)如用戶端驗證的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1b31e-193">See hello [Open ID Connect spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) for details on client authentication.</span></span>

<span data-ttu-id="1b31e-194">hello 下列範例顯示使用憑證認證的程式碼授與權杖的要求：</span><span class="sxs-lookup"><span data-stu-id="1b31e-194">hello following example shows a request for code grant token with certificate credential:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

<span data-ttu-id="1b31e-195">程式碼授與權杖回應的範例︰</span><span class="sxs-lookup"><span data-stu-id="1b31e-195">An example response for code grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a><span data-ttu-id="1b31e-196">處理程式碼授與權杖回應</span><span class="sxs-lookup"><span data-stu-id="1b31e-196">Handle code grant token response</span></span>
<span data-ttu-id="1b31e-197">成功的語彙基元回應包含 hello （使用者 + 應用程式） 存取權杖的 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1b31e-197">A successful token response contains hello (user + app) access token for Azure Resource Manager.</span></span> <span data-ttu-id="1b31e-198">您的應用程式會使用代表 hello 使用者此存取權杖 tooaccess 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1b31e-198">Your application uses this access token tooaccess Resource Manager on behalf of hello user.</span></span> <span data-ttu-id="1b31e-199">Azure AD 所簽發存取語彙基元的 hello 存留期為一小時。</span><span class="sxs-lookup"><span data-stu-id="1b31e-199">hello lifetime of access tokens issued by Azure AD is one hour.</span></span> <span data-ttu-id="1b31e-200">不太 web 應用程式需要 toorenew hello （使用者 + 應用程式） 存取權杖。</span><span class="sxs-lookup"><span data-stu-id="1b31e-200">It is unlikely that your web application needs toorenew hello (user + app) access token.</span></span> <span data-ttu-id="1b31e-201">如果它需要 toorenew hello 存取權杖時，使用您的應用程式收到 hello 權杖回應中的 hello 重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="1b31e-201">If it needs toorenew hello access token, use hello refresh token that your application receives in hello token response.</span></span> <span data-ttu-id="1b31e-202">張貼 OAuth2.0 語彙基元要求 toohello Azure AD 權杖端點：</span><span class="sxs-lookup"><span data-stu-id="1b31e-202">Post an OAuth2.0 Token Request toohello Azure AD Token endpoint:</span></span>

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

<span data-ttu-id="1b31e-203">hello 參數 toouse 與 hello 重新整理要求中有描述[重新整理 hello 存取權杖](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-203">hello parameters toouse with hello refresh request are described in [refreshing hello access token](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).</span></span>

<span data-ttu-id="1b31e-204">hello 下列範例顯示如何 toouse hello 重新整理權杖：</span><span class="sxs-lookup"><span data-stu-id="1b31e-204">hello following example shows how toouse hello refresh token:</span></span>

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

<span data-ttu-id="1b31e-205">雖然重新整理語彙基元可以用的 tooget 新存取權杖的 Azure 資源管理員，他們並不適合您的應用程式的離線存取。</span><span class="sxs-lookup"><span data-stu-id="1b31e-205">Although refresh tokens can be used tooget new access tokens for Azure Resource Manager, they are not suitable for offline access by your application.</span></span> <span data-ttu-id="1b31e-206">hello 重新整理權杖存留期受到限制，而且重新整理權杖是繫結的 toohello 使用者。</span><span class="sxs-lookup"><span data-stu-id="1b31e-206">hello refresh tokens lifetime is limited, and refresh tokens are bound toohello user.</span></span> <span data-ttu-id="1b31e-207">如果 hello 使用者離開組織 hello，hello 應用程式使用 hello 重新整理權杖會失去存取權。</span><span class="sxs-lookup"><span data-stu-id="1b31e-207">If hello user leaves hello organization, hello application using hello refresh token loses access.</span></span> <span data-ttu-id="1b31e-208">這個方法不是適用於應用程式供小組 toomanage 他們的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1b31e-208">This approach isn't suitable for applications that are used by teams toomanage their Azure resources.</span></span>

## <a name="check-if-user-can-assign-access-toosubscription"></a><span data-ttu-id="1b31e-209">請檢查使用者可指派給存取 toosubscription</span><span class="sxs-lookup"><span data-stu-id="1b31e-209">Check if user can assign access toosubscription</span></span>
<span data-ttu-id="1b31e-210">您的應用程式現在具有代表 hello 使用者語彙基元 tooaccess Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="1b31e-210">Your application now has a token tooaccess Azure Resource Manager on behalf of hello user.</span></span> <span data-ttu-id="1b31e-211">hello 下一個步驟是 tooconnect 應用程式 toohello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b31e-211">hello next step is tooconnect your app toohello subscription.</span></span> <span data-ttu-id="1b31e-212">連接之後，您的應用程式可以管理這些訂閱 hello 使用者不存在，即使 （長期離線存取）。</span><span class="sxs-lookup"><span data-stu-id="1b31e-212">After connecting, your app can manage those subscriptions even when hello user isn't present (long-term offline access).</span></span>

<span data-ttu-id="1b31e-213">每個訂用帳戶 tooconnect，來呼叫 hello[資源管理員清單權限](https://docs.microsoft.com/rest/api/authorization/permissions)API toodetermine hello 使用者是否擁有存取 hello 訂用帳戶的管理權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-213">For each subscription tooconnect, call hello [Resource Manager list permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine whether hello user has access management rights for hello subscription.</span></span>

<span data-ttu-id="1b31e-214">hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44)的 hello ASP.NET MVC 範例應用程式的方法會實作此呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b31e-214">hello [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) method of hello ASP.NET MVC sample app implements this call.</span></span>

<span data-ttu-id="1b31e-215">下列範例會示範如何 hello toorequest 訂用帳戶的使用者的權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-215">hello following example shows how toorequest a user's permissions on a subscription.</span></span> <span data-ttu-id="1b31e-216">83cfe939-2402-4581-b761-4f59b0a041e4 是 hello hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-216">83cfe939-2402-4581-b761-4f59b0a041e4 is hello id of hello subscription.</span></span>

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

<span data-ttu-id="1b31e-217">訂用帳戶的 hello 回應 tooget 使用者的權限的範例是：</span><span class="sxs-lookup"><span data-stu-id="1b31e-217">An example of hello response tooget user's permissions on subscription is:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

<span data-ttu-id="1b31e-218">hello 權限應用程式開發介面會傳回多個權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-218">hello permissions API returns multiple permissions.</span></span> <span data-ttu-id="1b31e-219">每個權限包含允許的動作 (actions) 和不允許的動作 (notactions)。</span><span class="sxs-lookup"><span data-stu-id="1b31e-219">Each permission consists of allowed actions (actions) and disallowed actions (notactions).</span></span> <span data-ttu-id="1b31e-220">如果動作是否存在於 hello 允許的任何權限的動作清單以及 hello notactions 該權限清單中不存在，hello 使用者是否允許 tooperform 該動作。</span><span class="sxs-lookup"><span data-stu-id="1b31e-220">If an action is present in hello allowed actions list of any permission and not present in hello notactions list of that permission, hello user is allowed tooperform that action.</span></span> <span data-ttu-id="1b31e-221">**microsoft.authorization/roleassignments/write** hello 動作，授與存取管理權利。</span><span class="sxs-lookup"><span data-stu-id="1b31e-221">**microsoft.authorization/roleassignments/write** is hello action that that grants access management rights.</span></span> <span data-ttu-id="1b31e-222">您的應用程式必須剖析 hello 權限結果 toolook regex 相符項目在 hello 動作和每個權限的 notactions 中此動作字串。</span><span class="sxs-lookup"><span data-stu-id="1b31e-222">Your application must parse hello permissions result toolook for a regex match on this action string in hello actions and notactions of each permission.</span></span>

## <a name="get-app-only-access-token"></a><span data-ttu-id="1b31e-223">取得僅限應用程式存取權杖</span><span class="sxs-lookup"><span data-stu-id="1b31e-223">Get app-only access token</span></span>
<span data-ttu-id="1b31e-224">現在，您知道如果 hello 使用者可以指派存取 toohello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b31e-224">Now, you know if hello user can assign access toohello Azure subscription.</span></span> <span data-ttu-id="1b31e-225">hello 後續的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="1b31e-225">hello next steps are:</span></span>

1. <span data-ttu-id="1b31e-226">指派 hello 訂用帳戶的 hello 適當 RBAC 角色 tooyour 應用程式的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-226">Assign hello appropriate RBAC role tooyour application's identity on hello subscription.</span></span>
2. <span data-ttu-id="1b31e-227">藉由查詢 hello 訂用帳戶上的 hello 應用程式的權限，或藉由存取資源管理員使用僅限應用程式的權杖驗證 hello 存取指派。</span><span class="sxs-lookup"><span data-stu-id="1b31e-227">Validate hello access assignment by querying for hello Application's permission on hello subscription or by accessing Resource Manager using app-only token.</span></span>
3. <span data-ttu-id="1b31e-228">您的應用程式 「 已連線的訂閱 」 資料結構-保存 hello 識別碼 hello 訂用帳戶中的記錄 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="1b31e-228">Record hello connection in your applications "connected subscriptions" data structure - persisting hello id of hello subscription.</span></span>

<span data-ttu-id="1b31e-229">讓我們來看靠近 hello 第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="1b31e-229">Let's look closer at hello first step.</span></span> <span data-ttu-id="1b31e-230">tooassign hello 適當 RBAC 角色 toohello 應用程式的身分識別，您必須決定：</span><span class="sxs-lookup"><span data-stu-id="1b31e-230">tooassign hello appropriate RBAC role toohello application's identity, you must determine:</span></span>

* <span data-ttu-id="1b31e-231">hello hello 使用者的 Azure Active Directory 中的應用程式的身分識別的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-231">hello object id of your application's identity in hello user's Azure Active Directory</span></span>
* <span data-ttu-id="1b31e-232">hello hello RBAC 角色應用程式所需 hello 訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-232">hello identifier of hello RBAC role that your application requires on hello subscription</span></span>

<span data-ttu-id="1b31e-233">當您的應用程式驗證來自 Azure AD 的使用者時，它會在該 Azure AD 中建立應用程式的服務主體物件。</span><span class="sxs-lookup"><span data-stu-id="1b31e-233">When your application authenticates a user from an Azure AD, it creates a service principal object for your application in that Azure AD.</span></span> <span data-ttu-id="1b31e-234">Azure 可讓 RBAC 角色 toobe 指派 tooservice 主體 toogrant 直接存取 toocorresponding 應用程式上的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="1b31e-234">Azure allows RBAC roles toobe assigned tooservice principals toogrant direct access toocorresponding applications on Azure resources.</span></span> <span data-ttu-id="1b31e-235">我們希望 toodo 此動作即完全相同。</span><span class="sxs-lookup"><span data-stu-id="1b31e-235">This action is exactly what we wish toodo.</span></span> <span data-ttu-id="1b31e-236">查詢 hello Azure AD Graph API toodetermine hello hello 服務主體識別碼 hello 登入的使用者在應用程式的 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="1b31e-236">Query hello Azure AD Graph API toodetermine hello identifier of hello service principal of your application in hello signed-in user's Azure AD.</span></span>

<span data-ttu-id="1b31e-237">您只需要存取權杖的 Azure 資源管理員-您需要新的存取語彙基元 toocall hello Azure AD Graph API。</span><span class="sxs-lookup"><span data-stu-id="1b31e-237">You only have an access token for Azure Resource Manager - you need a new access token toocall hello Azure AD Graph API.</span></span> <span data-ttu-id="1b31e-238">在 Azure AD 中的每個應用程式有權限 tooquery 它自己的服務主體物件，因此僅限應用程式的存取權杖已足夠。</span><span class="sxs-lookup"><span data-stu-id="1b31e-238">Every application in Azure AD has permission tooquery its own service principal object, so an app-only access token is sufficient.</span></span>

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a><span data-ttu-id="1b31e-239">取得 Azure AD Graph API 的僅限應用程式存取權杖</span><span class="sxs-lookup"><span data-stu-id="1b31e-239">Get app-only access token for Azure AD Graph API</span></span>
<span data-ttu-id="1b31e-240">tooauthenticate 應用程式，並取得語彙基元 tooAzure AD Graph API，發出的用戶端認證授與 OAuth2.0 流程語彙基元要求 tooAzure AD 權杖端點 (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/語彙基元**).</span><span class="sxs-lookup"><span data-stu-id="1b31e-240">tooauthenticate your app and get a token tooAzure AD Graph API, issue a Client Credential Grant OAuth2.0 flow token request tooAzure AD token endpoint (**https://login.microsoftonline.com/{directory_domain_name}/OAuth2/Token**).</span></span>

<span data-ttu-id="1b31e-241">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs)方法的 ASP.net MVC 範例應用程式取得僅限應用程式的存取權杖以供使用 Graph API 的 hello hello Active Directory Authentication Library for.NET。</span><span class="sxs-lookup"><span data-stu-id="1b31e-241">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) method of hello ASP.net MVC sample application gets an app-only access token for Graph API using hello Active Directory Authentication Library for .NET.</span></span>

<span data-ttu-id="1b31e-242">hello 查詢字串參數可用於此要求所述 hello[要求存取權杖](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token)主題。</span><span class="sxs-lookup"><span data-stu-id="1b31e-242">hello query string parameters that are available for this request are described in hello [Request an Access Token](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) topic.</span></span>

<span data-ttu-id="1b31e-243">用戶端認證授與權杖要求範例︰</span><span class="sxs-lookup"><span data-stu-id="1b31e-243">An example request for client credential grant token:</span></span>

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

<span data-ttu-id="1b31e-244">用戶端認證授與權杖回應範例︰</span><span class="sxs-lookup"><span data-stu-id="1b31e-244">An example response for client credential grant token:</span></span>

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a><span data-ttu-id="1b31e-245">取得使用者 Azure AD 中的應用程式服務主體的 ObjectId</span><span class="sxs-lookup"><span data-stu-id="1b31e-245">Get ObjectId of application service principal in user Azure AD</span></span>
<span data-ttu-id="1b31e-246">現在，使用 hello 僅限應用程式的存取語彙基元 tooquery hello [Azure AD Graph 服務主體](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity)API toodetermine hello hello 目錄中的 hello 應用程式的服務主體的物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-246">Now, use hello app-only access token tooquery hello [Azure AD Graph Service Principals](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API toodetermine hello Object Id of hello application's service principal in hello directory.</span></span>

<span data-ttu-id="1b31e-247">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#)的 hello ASP.net MVC 範例應用程式的方法會實作此呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b31e-247">hello [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) method of hello ASP.net MVC sample application implements this call.</span></span>

<span data-ttu-id="1b31e-248">下列範例會示範如何 hello toorequest 應用程式的服務主體。</span><span class="sxs-lookup"><span data-stu-id="1b31e-248">hello following example shows how toorequest an application's service principal.</span></span> <span data-ttu-id="1b31e-249">a0448380-c346-4f9f-b897-c18733de9394 是 hello 用戶端識別碼 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-249">a0448380-c346-4f9f-b897-c18733de9394 is hello client id of hello application.</span></span>

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

<span data-ttu-id="1b31e-250">hello 下列範例顯示的應用程式服務的回應 toohello 要求主體</span><span class="sxs-lookup"><span data-stu-id="1b31e-250">hello following example shows a response toohello request for an application's service principal</span></span>

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a><span data-ttu-id="1b31e-251">取得 Azure RBAC 角色識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-251">Get Azure RBAC role identifier</span></span>
<span data-ttu-id="1b31e-252">tooassign hello 適當 RBAC 角色 tooyour 服務主體，您必須決定 hello hello Azure rbac 進行角色識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-252">tooassign hello appropriate RBAC role tooyour service principal, you must determine hello identifier of hello Azure RBAC role.</span></span>

<span data-ttu-id="1b31e-253">hello 右 RBAC 角色應用程式：</span><span class="sxs-lookup"><span data-stu-id="1b31e-253">hello right RBAC role for your application:</span></span>

* <span data-ttu-id="1b31e-254">如果您的應用程式只會監視 hello 訂用帳戶，而不進行任何變更，則需要只有 hello 訂用帳戶的讀取器權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-254">If your application only monitors hello subscription, without making any changes, it requires only reader permissions on hello subscription.</span></span> <span data-ttu-id="1b31e-255">指派 hello**讀取器**角色。</span><span class="sxs-lookup"><span data-stu-id="1b31e-255">Assign hello **Reader** role.</span></span>
* <span data-ttu-id="1b31e-256">如果您的應用程式為您管理 Azure 的 hello 訂用帳戶，建立/修改/刪除實體，它需要下列其中一個 hello 參與者權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-256">If your application manages Azure hello subscription, creating/modifying/deleting entities, it requires one of hello contributor permissions.</span></span>
  * <span data-ttu-id="1b31e-257">toomanage 特定類型的資源，指派 hello 特定資源參與者角色 （虛擬機器參與者、 虛擬網路參與者、 儲存體帳戶參與者等）</span><span class="sxs-lookup"><span data-stu-id="1b31e-257">toomanage a particular type of resource, assign hello resource-specific contributor roles (Virtual Machine Contributor, Virtual Network Contributor, Storage Account Contributor, etc.)</span></span>
  * <span data-ttu-id="1b31e-258">toomanage 任何資源類型、 指派 hello**參與者**角色。</span><span class="sxs-lookup"><span data-stu-id="1b31e-258">toomanage any resource type, assign hello **Contributor** role.</span></span>

<span data-ttu-id="1b31e-259">hello 應用程式的角色指派是可見的 toousers，因此選取 hello 最低所需的權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-259">hello role assignment for your application is visible toousers, so select hello least-required privilege.</span></span>

<span data-ttu-id="1b31e-260">呼叫 hello[資源管理員角色定義 API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist 所有 Azure rbac 進行角色和搜尋然後都逐一 hello 結果 toofind hello 預期角色定義的名稱。</span><span class="sxs-lookup"><span data-stu-id="1b31e-260">Call hello [Resource Manager role definition API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist all Azure RBAC roles and search then iterate over hello result toofind hello desired role definition by name.</span></span>

<span data-ttu-id="1b31e-261">hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246)的 hello ASP.net MVC 範例應用程式的方法會實作此呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b31e-261">hello [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) method of hello ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="1b31e-262">hello 下列要求的範例會示範如何 tooget Azure rbac 進行角色識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-262">hello following request example shows how tooget Azure RBAC role identifier.</span></span> <span data-ttu-id="1b31e-263">09cbd307-aa71-4aca-b346-5f253e6e3ebb 是 hello hello 訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="1b31e-263">09cbd307-aa71-4aca-b346-5f253e6e3ebb is hello id of hello subscription.</span></span>

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

<span data-ttu-id="1b31e-264">hello 回應 hello 遵循格式為：</span><span class="sxs-lookup"><span data-stu-id="1b31e-264">hello response is in hello following format:</span></span>

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

<span data-ttu-id="1b31e-265">您不需要 toocall 持續不斷上的這個 API。</span><span class="sxs-lookup"><span data-stu-id="1b31e-265">You do not need toocall this API on an ongoing basis.</span></span> <span data-ttu-id="1b31e-266">一旦您判定 hello hello 角色定義的已知 GUID，您可以建構 hello 角色定義 id 為：</span><span class="sxs-lookup"><span data-stu-id="1b31e-266">Once you've determined hello well-known GUID of hello role definition, you can construct hello role definition id as:</span></span>

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

<span data-ttu-id="1b31e-267">以下是常用的內建角色的 hello 已知 guid:</span><span class="sxs-lookup"><span data-stu-id="1b31e-267">Here are hello well-known guids of commonly used built-in roles:</span></span>

| <span data-ttu-id="1b31e-268">角色</span><span class="sxs-lookup"><span data-stu-id="1b31e-268">Role</span></span> | <span data-ttu-id="1b31e-269">Guid</span><span class="sxs-lookup"><span data-stu-id="1b31e-269">Guid</span></span> |
| --- | --- |
| <span data-ttu-id="1b31e-270">讀取器</span><span class="sxs-lookup"><span data-stu-id="1b31e-270">Reader</span></span> |<span data-ttu-id="1b31e-271">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="1b31e-271">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |
| <span data-ttu-id="1b31e-272">參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-272">Contributor</span></span> |<span data-ttu-id="1b31e-273">b24988ac-6180-42a0-ab88-20f7382dd24c</span><span class="sxs-lookup"><span data-stu-id="1b31e-273">b24988ac-6180-42a0-ab88-20f7382dd24c</span></span> |
| <span data-ttu-id="1b31e-274">虛擬機器參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-274">Virtual Machine Contributor</span></span> |<span data-ttu-id="1b31e-275">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span><span class="sxs-lookup"><span data-stu-id="1b31e-275">d73bb868-a0df-4d4d-bd69-98a00b01fccb</span></span> |
| <span data-ttu-id="1b31e-276">虛擬網路參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-276">Virtual Network Contributor</span></span> |<span data-ttu-id="1b31e-277">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span><span class="sxs-lookup"><span data-stu-id="1b31e-277">b34d265f-36f7-4a0d-a4d4-e158ca92e90f</span></span> |
| <span data-ttu-id="1b31e-278">儲存體帳戶參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-278">Storage Account Contributor</span></span> |<span data-ttu-id="1b31e-279">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span><span class="sxs-lookup"><span data-stu-id="1b31e-279">86e8f5dc-a6e9-4c67-9d15-de283e8eac25</span></span> |
| <span data-ttu-id="1b31e-280">網站參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-280">Website Contributor</span></span> |<span data-ttu-id="1b31e-281">de139f84-1756-47ae-9be6-808fbbe84772</span><span class="sxs-lookup"><span data-stu-id="1b31e-281">de139f84-1756-47ae-9be6-808fbbe84772</span></span> |
| <span data-ttu-id="1b31e-282">Web 方案參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-282">Web Plan Contributor</span></span> |<span data-ttu-id="1b31e-283">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span><span class="sxs-lookup"><span data-stu-id="1b31e-283">2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b</span></span> |
| <span data-ttu-id="1b31e-284">SQL Server 參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-284">SQL Server Contributor</span></span> |<span data-ttu-id="1b31e-285">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span><span class="sxs-lookup"><span data-stu-id="1b31e-285">6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437</span></span> |
| <span data-ttu-id="1b31e-286">SQL DB 參與者</span><span class="sxs-lookup"><span data-stu-id="1b31e-286">SQL DB Contributor</span></span> |<span data-ttu-id="1b31e-287">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span><span class="sxs-lookup"><span data-stu-id="1b31e-287">9b7fa17d-e63e-47b0-bb0a-15c516ac86ec</span></span> |

### <a name="assign-rbac-role-tooapplication"></a><span data-ttu-id="1b31e-288">指派 RBAC 角色 tooapplication</span><span class="sxs-lookup"><span data-stu-id="1b31e-288">Assign RBAC role tooapplication</span></span>
<span data-ttu-id="1b31e-289">您擁有所需的所有 tooassign hello 適當 RBAC 角色 tooyour 服務主體使用 hello[資源管理員 建立角色指派](https://docs.microsoft.com/rest/api/authorization/roleassignments)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1b31e-289">You have everything you need tooassign hello appropriate RBAC role tooyour service principal by using hello [Resource Manager create role assignment](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.</span></span>

<span data-ttu-id="1b31e-290">hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170)的 hello ASP.net MVC 範例應用程式的方法會實作此呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b31e-290">hello [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) method of hello ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="1b31e-291">範例要求 tooassign RBAC 角色 tooapplication:</span><span class="sxs-lookup"><span data-stu-id="1b31e-291">An example request tooassign RBAC role tooapplication:</span></span>

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

<span data-ttu-id="1b31e-292">在 hello 要求中，會使用下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b31e-292">In hello request, hello following values are used:</span></span>

| <span data-ttu-id="1b31e-293">Guid</span><span class="sxs-lookup"><span data-stu-id="1b31e-293">Guid</span></span> | <span data-ttu-id="1b31e-294">說明</span><span class="sxs-lookup"><span data-stu-id="1b31e-294">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b31e-295">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span><span class="sxs-lookup"><span data-stu-id="1b31e-295">09cbd307-aa71-4aca-b346-5f253e6e3ebb</span></span> |<span data-ttu-id="1b31e-296">hello hello 訂閱識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-296">hello id of hello subscription</span></span> |
| <span data-ttu-id="1b31e-297">c3097b31-7309-4c59-b4e3-770f8406bad2</span><span class="sxs-lookup"><span data-stu-id="1b31e-297">c3097b31-7309-4c59-b4e3-770f8406bad2</span></span> |<span data-ttu-id="1b31e-298">hello hello hello 應用程式的服務主體的物件識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-298">hello object id of hello service principal of hello application</span></span> |
| <span data-ttu-id="1b31e-299">acdd72a7-3385-48ef-bd42-f606fba81ae7</span><span class="sxs-lookup"><span data-stu-id="1b31e-299">acdd72a7-3385-48ef-bd42-f606fba81ae7</span></span> |<span data-ttu-id="1b31e-300">hello hello 讀取器角色識別碼</span><span class="sxs-lookup"><span data-stu-id="1b31e-300">hello id of hello reader role</span></span> |
| <span data-ttu-id="1b31e-301">4f87261d-2816-465d-8311-70a27558df4c</span><span class="sxs-lookup"><span data-stu-id="1b31e-301">4f87261d-2816-465d-8311-70a27558df4c</span></span> |<span data-ttu-id="1b31e-302">新的 guid 建立 hello 新角色指派</span><span class="sxs-lookup"><span data-stu-id="1b31e-302">a new guid created for hello new role assignment</span></span> |

<span data-ttu-id="1b31e-303">hello 回應 hello 遵循格式為：</span><span class="sxs-lookup"><span data-stu-id="1b31e-303">hello response is in hello following format:</span></span>

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a><span data-ttu-id="1b31e-304">取得 Azure Resource Manager 的僅限應用程式存取權杖</span><span class="sxs-lookup"><span data-stu-id="1b31e-304">Get app-only access token for Azure Resource Manager</span></span>
<span data-ttu-id="1b31e-305">toovalidate 該應用程式所需的 hello 存取 hello 訂用帳戶，請使用僅限應用程式的權杖 hello 訂用帳戶上執行的測試工作。</span><span class="sxs-lookup"><span data-stu-id="1b31e-305">toovalidate that app has hello desired access on hello subscription, perform a test task on hello subscription using an app-only token.</span></span>

<span data-ttu-id="1b31e-306">tooget 僅限應用程式的存取權杖，請依照指示執行區段[取得 Azure AD Graph api 的僅限應用程式的存取權杖](#app-azure-ad-graph)，具有不同的值為 hello resource 參數：</span><span class="sxs-lookup"><span data-stu-id="1b31e-306">tooget an app-only access token, follow instructions from section [Get app-only access token for Azure AD Graph API](#app-azure-ad-graph), with a different value for hello resource parameter:</span></span>

    https://management.core.windows.net/

<span data-ttu-id="1b31e-307">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) hello ASP.NET MVC 範例應用程式取得僅限應用程式的存取語彙基元的 Azure 資源管理員使用的方法 hello Active Directory Authentication Library for.net。</span><span class="sxs-lookup"><span data-stu-id="1b31e-307">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of hello ASP.NET MVC sample application gets an app-only access token for Azure Resource Manager using hello Active Directory Authentication Library for .net.</span></span>

#### <a name="get-applications-permissions-on-subscription"></a><span data-ttu-id="1b31e-308">取得訂用帳戶上的應用程式權限</span><span class="sxs-lookup"><span data-stu-id="1b31e-308">Get Application's Permissions on Subscription</span></span>
<span data-ttu-id="1b31e-309">您的應用程式具有 hello 的 toocheck 想要針對 Azure 訂用帳戶的存取，您可能也會呼叫 hello[資源管理員 」 權限](https://docs.microsoft.com/rest/api/authorization/permissions)應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="1b31e-309">toocheck that your application has hello desired access on an Azure subscription, you may also call hello [Resource Manager Permissions](https://docs.microsoft.com/rest/api/authorization/permissions) API.</span></span> <span data-ttu-id="1b31e-310">這個方法很類似 toohow 您決定 hello 使用者是否具有 hello 訂用帳戶的管理存取權限。</span><span class="sxs-lookup"><span data-stu-id="1b31e-310">This approach is similar toohow you determined whether hello user has Access Management rights for hello subscription.</span></span> <span data-ttu-id="1b31e-311">不過，這次呼叫 hello 權限應用程式開發介面使用 hello 上一個步驟中收到 hello 僅限應用程式的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="1b31e-311">However, this time, call hello permissions API with hello app-only access token that you received in hello previous step.</span></span>

<span data-ttu-id="1b31e-312">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110)的 hello ASP.NET MVC 範例應用程式的方法會實作此呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b31e-312">hello [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) method of hello ASP.NET MVC sample app implements this call.</span></span>

## <a name="manage-connected-subscriptions"></a><span data-ttu-id="1b31e-313">管理連接的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1b31e-313">Manage connected subscriptions</span></span>
<span data-ttu-id="1b31e-314">當 hello 適當 RBAC 的角色指派 tooyour 應用程式的服務主體 hello 訂用帳戶時，您的應用程式可以保留監視/管理 Azure 資源管理員的使用僅限應用程式的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="1b31e-314">When hello appropriate RBAC role is assigned tooyour application's service principal on hello subscription, your application can keep monitoring/managing it using app-only access tokens for Azure Resource Manager.</span></span>

<span data-ttu-id="1b31e-315">如果訂用帳戶擁有者移除您的應用程式使用 hello 傳統入口網站或命令列工具，您的應用程式的角色指派是不再能 tooaccess 該訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b31e-315">If a subscription owner removes your application's role assignment using hello classic portal or command-line tools, your application is no longer able tooaccess that subscription.</span></span> <span data-ttu-id="1b31e-316">在此情況下，您應通知 hello 使用者 hello 與 hello 訂用帳戶的連接已嚴重損毀來自外部的 hello 應用程式授與他們選項太 「 修復 」 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="1b31e-316">In that case, you should notify hello user that hello connection with hello subscription was severed from outside hello application and give them an option too"repair" hello connection.</span></span> <span data-ttu-id="1b31e-317">「 修復 」 只會重新建立 hello 離線已刪除的角色指派。</span><span class="sxs-lookup"><span data-stu-id="1b31e-317">"Repair" would simply re-create hello role assignment that was deleted offline.</span></span>

<span data-ttu-id="1b31e-318">就如同您啟用 hello 使用者 tooconnect 訂閱 tooyour 應用程式，您必須太允許 hello 使用者 toodisconnect 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b31e-318">Just as you enabled hello user tooconnect subscriptions tooyour application, you must allow hello user toodisconnect subscriptions too.</span></span> <span data-ttu-id="1b31e-319">從存取管理的觀點，中斷連線移除 hello hello 應用程式的服務主體具有 hello 訂用帳戶的角色指派的方式。</span><span class="sxs-lookup"><span data-stu-id="1b31e-319">From an access management point of view, disconnect means removing hello role assignment that hello application's service principal has on hello subscription.</span></span> <span data-ttu-id="1b31e-320">（選擇性） 可能太移除 hello hello 訂用帳戶的應用程式中的任何狀態。</span><span class="sxs-lookup"><span data-stu-id="1b31e-320">Optionally, any state in hello application for hello subscription might be removed too.</span></span>
<span data-ttu-id="1b31e-321">只有具有存取 hello 訂用帳戶的管理權限的使用者都能 toodisconnect hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b31e-321">Only users with access management permission on hello subscription are able toodisconnect hello subscription.</span></span>

<span data-ttu-id="1b31e-322">hello [RevokeRoleFromServicePrincipalOnSubscription 方法](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200)hello ASP.net MVC 的範例應用程式會實作此呼叫。</span><span class="sxs-lookup"><span data-stu-id="1b31e-322">hello [RevokeRoleFromServicePrincipalOnSubscription method](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) of hello ASP.net MVC sample app implements this call.</span></span>

<span data-ttu-id="1b31e-323">大功告成，使用者現在能使用您的應用程式來輕鬆連接及管理其 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b31e-323">That's it - users can now easily connect and manage their Azure subscriptions with your application.</span></span>
