---
title: "aaaAuthenticate 與 Mobile Engagement REST Api"
description: "描述如何使用 Azure Mobile Engagement REST Api tooauthenticate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="4579b-103">使用 Mobile Engagement REST API 進行驗證</span><span class="sxs-lookup"><span data-stu-id="4579b-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="4579b-104">概觀</span><span class="sxs-lookup"><span data-stu-id="4579b-104">Overview</span></span>
<span data-ttu-id="4579b-105">本文件說明如何 tooget 有效的 AAD Oauth 語彙基元 tooauthenticate 以 hello Mobile Engagement REST Api。</span><span class="sxs-lookup"><span data-stu-id="4579b-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="4579b-106">已假設您具備有效的 Azure 訂用帳戶，也已使用其中一個 [開發人員教學課程](mobile-engagement-windows-store-dotnet-get-started.md)建立 Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4579b-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="4579b-107">驗證</span><span class="sxs-lookup"><span data-stu-id="4579b-107">Authentication</span></span>
<span data-ttu-id="4579b-108">使用 Microsoft Azure Active Directory 型的 OAuth 權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4579b-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="4579b-109">在訂單 tooauthentication API 要求中，授權標頭必須加入屬於下列表單的 hello tooevery 要求：</span><span class="sxs-lookup"><span data-stu-id="4579b-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="4579b-110">Azure Active Directory 權杖會在 1 小時內過期。</span><span class="sxs-lookup"><span data-stu-id="4579b-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="4579b-111">有數種方式 tooget 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="4579b-111">There are several ways tooget a token.</span></span> <span data-ttu-id="4579b-112">Hello Api 通常稱為從雲端服務，因為您想 toouse API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="4579b-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="4579b-113">在 Azure 術語中，API 金鑰稱為「服務主體密碼」。</span><span class="sxs-lookup"><span data-stu-id="4579b-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="4579b-114">hello 下列程序說明其中一種方式 toosetting 它以手動方式啟動。</span><span class="sxs-lookup"><span data-stu-id="4579b-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="4579b-115">單次設定 (使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="4579b-115">One-time setup (using script)</span></span>
<span data-ttu-id="4579b-116">您應該遵循 hello 組 tooperform hello 安裝程式需要 hello 安裝程式的最小時間，但是會使用 hello 最所允許的預設值的 PowerShell 指令碼中使用下列指示。</span><span class="sxs-lookup"><span data-stu-id="4579b-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="4579b-117">（選擇性） 您也可以遵循 hello 中的 hello 指示[手動安裝](mobile-engagement-api-authentication-manual.md)hello Azure 入口網站直接與不要進行更細微的組態執行此作業。</span><span class="sxs-lookup"><span data-stu-id="4579b-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="4579b-118">取得 hello 最新版本的 Azure PowerShell，從[這裡](http://aka.ms/webpi-azps)。</span><span class="sxs-lookup"><span data-stu-id="4579b-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="4579b-119">如需有關 hello 下載指示的詳細資訊，您可以看到這[連結](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4579b-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="4579b-120">使用 hello 下列 Azure PowerShell 安裝之後，命令 tooensure 您擁有 hello **Azure 模組**安裝：</span><span class="sxs-lookup"><span data-stu-id="4579b-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="4579b-121">a.</span><span class="sxs-lookup"><span data-stu-id="4579b-121">a.</span></span> <span data-ttu-id="4579b-122">確定在 hello 可用的模組清單中的 hello Azure PowerShell 模組可用。</span><span class="sxs-lookup"><span data-stu-id="4579b-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![可用的 Azure 模組][1]
   
    <span data-ttu-id="4579b-124">b.</span><span class="sxs-lookup"><span data-stu-id="4579b-124">b.</span></span> <span data-ttu-id="4579b-125">如果您找不到 hello Azure PowerShell 模組清單上方的 hello 中您會需要 toorun hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4579b-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="4579b-126">登入 toohello 從 PowerShell 的 Azure 資源管理員執行 hello 下列命令，並提供您的 Azure 帳戶使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="4579b-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="4579b-127">如果您有多個訂閱，您應該執行 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="4579b-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="4579b-128">a.</span><span class="sxs-lookup"><span data-stu-id="4579b-128">a.</span></span> <span data-ttu-id="4579b-129">Toouse 取得您所有的訂閱和複製 hello hello 您想要的訂用帳戶的訂用帳戶 Id 的清單。</span><span class="sxs-lookup"><span data-stu-id="4579b-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="4579b-130">請確定此訂用帳戶是具有相同 hello 您 Mobile Engagement 應用程式的 hello 與使用 toointeract hello 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4579b-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="4579b-131">b.</span><span class="sxs-lookup"><span data-stu-id="4579b-131">b.</span></span> <span data-ttu-id="4579b-132">Hello 執行的下列命令提供 hello SubscriptionId tooconfigure hello 訂用帳戶 toobe 使用。</span><span class="sxs-lookup"><span data-stu-id="4579b-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="4579b-133">複製 hello 的 hello 文字[新增 AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1)指令碼 tooyour 本機電腦，然後將它儲存為 PowerShell 指令程式 (例如`APIAuth.ps1`) 並執行它`.\APIAuth.ps1`。</span><span class="sxs-lookup"><span data-stu-id="4579b-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="4579b-134">hello 指令碼會要求您輸入的 tooprovide **principalName**。</span><span class="sxs-lookup"><span data-stu-id="4579b-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="4579b-135">您想 toouse toocreate Active Directory 應用程式 (例如 APIAuth) 提供一個適合的名稱。</span><span class="sxs-lookup"><span data-stu-id="4579b-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="4579b-136">Hello 指令碼完成後，它會顯示 hello 下列四個值，您必須以程式設計方式使用 AD tooauthenticate，所以請確定 toocopy 它們。</span><span class="sxs-lookup"><span data-stu-id="4579b-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="4579b-137">**TenantId**、**SubscriptionId**、**ApplicationId** 及 **Secret**。</span><span class="sxs-lookup"><span data-stu-id="4579b-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="4579b-138">您將使用 TenantId 做為 `{TENANT_ID}`、使用 ApplicationId 做為 `{CLIENT_ID}`，並使用 Secret 做為 `{CLIENT_SECRET}`。</span><span class="sxs-lookup"><span data-stu-id="4579b-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4579b-139">預設的安全性原則可能會阻止您執行 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4579b-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="4579b-140">如果是這樣，您會暫時設定您執行 tooallow 指令碼執行原則使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="4579b-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="4579b-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="4579b-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="4579b-142">以下是 hello 組 PS 指令程式會如下。</span><span class="sxs-lookup"><span data-stu-id="4579b-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="4579b-143">請檢查 hello Azure 管理入口網站中，新的 AD 應用程式建立 hello 名稱您提供 toohello 指令碼呼叫**principalName**下**顯示我公司所擁有的應用程式**。</span><span class="sxs-lookup"><span data-stu-id="4579b-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="4579b-144">步驟 tooget 有效的語彙基元</span><span class="sxs-lookup"><span data-stu-id="4579b-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="4579b-145">以下列參數的 hello 呼叫 hello 應用程式開發介面，並請確定 tooreplace hello 租用戶\_識別碼、 用戶端\_識別碼和用戶端\_密碼：</span><span class="sxs-lookup"><span data-stu-id="4579b-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="4579b-146">**要求 URL** 為 https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token</span><span class="sxs-lookup"><span data-stu-id="4579b-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="4579b-147">**HTTP Content-Type 標頭** 為 *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="4579b-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="4579b-148">**HTTP 要求主體**為 grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="4579b-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="4579b-149">hello 下面是範例要求：</span><span class="sxs-lookup"><span data-stu-id="4579b-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="4579b-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="4579b-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="4579b-151">以下是範例回應：</span><span class="sxs-lookup"><span data-stu-id="4579b-151">Here is an example response:</span></span>
     
       <span data-ttu-id="4579b-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="4579b-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="4579b-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="4579b-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="4579b-154">這個範例包含 URL 編碼的 hello POST 參數，`resource`值實際上是`https://management.core.windows.net/`。</span><span class="sxs-lookup"><span data-stu-id="4579b-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="4579b-155">請小心 tooalso URL 編碼`{CLIENT_SECRET}`因為它可能包含特殊字元。</span><span class="sxs-lookup"><span data-stu-id="4579b-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="4579b-156">如需測試，您可以使用像是 [Fiddler](http://www.telerik.com/fiddler) 或 [Chrome Postman 擴充](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)的 HTTP 用戶端工具</span><span class="sxs-lookup"><span data-stu-id="4579b-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="4579b-157">現在每個應用程式開發介面呼叫，包括 hello 授權要求標頭：</span><span class="sxs-lookup"><span data-stu-id="4579b-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="4579b-158">如果您收到 401 狀態碼傳回，核取 hello 回應主體中，它可能在 hello 權杖到期時告訴您。</span><span class="sxs-lookup"><span data-stu-id="4579b-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="4579b-159">在此情況下，請取得新的權杖。</span><span class="sxs-lookup"><span data-stu-id="4579b-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="4579b-160">使用 hello 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="4579b-160">Using hello APIs</span></span>
<span data-ttu-id="4579b-161">現在您有有效的語彙基元時，您就準備 toomake hello API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="4579b-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="4579b-162">在每個 API 要求中，您必須使用 toopass 有效且未到期的語彙基元 hello 前一節中取得。</span><span class="sxs-lookup"><span data-stu-id="4579b-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="4579b-163">您將需要某些參數 tooplug 入 hello 要求 URI 可用來識別您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4579b-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="4579b-164">hello 要求 URI 看起來像下列 hello</span><span class="sxs-lookup"><span data-stu-id="4579b-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="4579b-165">tooget hello 參數，按一下您的應用程式名稱，然後按一下 儀表板，您會看到一個頁面，像是 hello 下列所有 hello 3 個參數。</span><span class="sxs-lookup"><span data-stu-id="4579b-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="4579b-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="4579b-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="4579b-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="4579b-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="4579b-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="4579b-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="4579b-169">**4**您的資源群組名稱即將 toobe **MobileEngagement**除非您建立一個新。</span><span class="sxs-lookup"><span data-stu-id="4579b-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI 參數][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="4579b-171">忽略 hello API 根位址，因為這是 hello 先前的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="4579b-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="4579b-172">如果您建立使用 Azure 傳統入口網站的 hello 應用程式則需要 toouse hello 應用程式資源名稱有別於 hello 應用程式名稱本身。</span><span class="sxs-lookup"><span data-stu-id="4579b-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="4579b-173">如果您建立 hello Azure 入口網站中的 hello 應用程式，您應該使用 hello 本身 （沒有應用程式資源名稱與 hello 新入口網站中建立的應用程式的應用程式名稱之間沒有差異） 的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="4579b-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



