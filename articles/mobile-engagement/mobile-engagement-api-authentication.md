---
title: "使用 Mobile Engagement REST API 進行驗證"
description: "描述如何使用 Azure Mobile Engagement REST API 進行驗證"
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
ms.openlocfilehash: b05181d9252c0a804648e01b4058019278ae5abe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="90cf2-103">使用 Mobile Engagement REST API 進行驗證</span><span class="sxs-lookup"><span data-stu-id="90cf2-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="90cf2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="90cf2-104">Overview</span></span>
<span data-ttu-id="90cf2-105">本文件說明如何取得有效的 AAD Oauth 權杖，以使用 Mobile Engagement REST API 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="90cf2-105">This document describes how to get a valid AAD Oauth token to authenticate with the Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="90cf2-106">已假設您具備有效的 Azure 訂用帳戶，也已使用其中一個 [開發人員教學課程](mobile-engagement-windows-store-dotnet-get-started.md)建立 Mobile Engagement 應用程式。</span><span class="sxs-lookup"><span data-stu-id="90cf2-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="90cf2-107">驗證</span><span class="sxs-lookup"><span data-stu-id="90cf2-107">Authentication</span></span>
<span data-ttu-id="90cf2-108">使用 Microsoft Azure Active Directory 型的 OAuth 權杖進行驗證。</span><span class="sxs-lookup"><span data-stu-id="90cf2-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="90cf2-109">為了驗證 API 要求，必須將授權標頭加入至每個要求，其格式如下：</span><span class="sxs-lookup"><span data-stu-id="90cf2-109">In order to authentication an API request, an authorization header must be added to every request which is of the following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="90cf2-110">Azure Active Directory 權杖會在 1 小時內過期。</span><span class="sxs-lookup"><span data-stu-id="90cf2-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="90cf2-111">有幾種方式可以取得權杖。</span><span class="sxs-lookup"><span data-stu-id="90cf2-111">There are several ways to get a token.</span></span> <span data-ttu-id="90cf2-112">因為通常會從雲端服務呼叫 API，所以您會想要使用 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="90cf2-112">Since the APIs are generally called from a cloud service, you want to use an API key.</span></span> <span data-ttu-id="90cf2-113">在 Azure 術語中，API 金鑰稱為「服務主體密碼」。</span><span class="sxs-lookup"><span data-stu-id="90cf2-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="90cf2-114">下列程序說明一種手動設定的方法。</span><span class="sxs-lookup"><span data-stu-id="90cf2-114">The following procedure describes one way to setting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="90cf2-115">單次設定 (使用指令碼)</span><span class="sxs-lookup"><span data-stu-id="90cf2-115">One-time setup (using script)</span></span>
<span data-ttu-id="90cf2-116">您應該遵循下列這組指示，使用 PowerShell 指令碼來執行安裝程式，該指令碼會利用最少時間進行安裝，但會使用最多允許的預設值。</span><span class="sxs-lookup"><span data-stu-id="90cf2-116">You should follow the set of instructions below to perform the setup using a PowerShell script which takes the minimum time for setup but uses the most permissible defaults.</span></span> <span data-ttu-id="90cf2-117">或者，您也可以依照 [手動安裝](mobile-engagement-api-authentication-manual.md) 中的指示來執行，以便從 Azure 入口網站直接執行此動作並進行更細微的設定。</span><span class="sxs-lookup"><span data-stu-id="90cf2-117">Optionally, you can also follow the instructions in the [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from the Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="90cf2-118">從 [此處](http://aka.ms/webpi-azps)取得最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="90cf2-118">Get the latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="90cf2-119">如需下載指示的詳細資訊，您可以查看這個 [連結](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="90cf2-119">For more information on the download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="90cf2-120">安裝 Azure PowerShell 之後，使用下列命令，以確保您已安裝 **Azure 模組** ︰</span><span class="sxs-lookup"><span data-stu-id="90cf2-120">Once Azure PowerShell is installed, use the following commands to ensure that you have the **Azure module** installed:</span></span>
   
    <span data-ttu-id="90cf2-121">a.</span><span class="sxs-lookup"><span data-stu-id="90cf2-121">a.</span></span> <span data-ttu-id="90cf2-122">確定 Azure PowerShell 模組可在可用模組清單中取得。</span><span class="sxs-lookup"><span data-stu-id="90cf2-122">Make sure the Azure PowerShell module is available in the list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![可用的 Azure 模組][1]
   
    <span data-ttu-id="90cf2-124">b.</span><span class="sxs-lookup"><span data-stu-id="90cf2-124">b.</span></span> <span data-ttu-id="90cf2-125">如果您在上述清單中找不到 Azure PowerShell 模組，則必須執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="90cf2-125">If you do not find the Azure PowerShell module in the above list then you need to run the following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="90cf2-126">從 PowerShell 登入 Azure Resource Manager，方法是執行下列命令，並提供您 Azure 帳戶的使用者名稱和密碼︰</span><span class="sxs-lookup"><span data-stu-id="90cf2-126">Login to the Azure Resource Manager from PowerShell by running the following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="90cf2-127">如果您擁有多個訂用帳戶，則您應該執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="90cf2-127">If you have multiple subscriptions then you should run the following:</span></span>
   
    <span data-ttu-id="90cf2-128">a.</span><span class="sxs-lookup"><span data-stu-id="90cf2-128">a.</span></span> <span data-ttu-id="90cf2-129">取得所有訂用帳戶的清單，並複製您想要使用的訂用帳戶的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="90cf2-129">Get a list of all your subscriptions and copy the SubscriptionId of the subscription you want to use.</span></span> <span data-ttu-id="90cf2-130">請確定此訂用帳戶是具有您想要使用 API 與 Mobile Engagement 應用程式進行互動的同一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="90cf2-130">Make sure this subscription is the same one which has the Mobile Engagement App which you are going to interact with using the APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="90cf2-131">b.</span><span class="sxs-lookup"><span data-stu-id="90cf2-131">b.</span></span> <span data-ttu-id="90cf2-132">執行下列命令提供訂用帳戶識別碼來設定要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="90cf2-132">Run the following command providing the SubscriptionId to configure the subscription to be used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="90cf2-133">將 [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) 指令碼的文字複製到本機電腦、將它儲存為 PowerShell Cmdlet (例如 `APIAuth.ps1`)，然後執行它 `.\APIAuth.ps1`。</span><span class="sxs-lookup"><span data-stu-id="90cf2-133">Copy the text for the [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script to your local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="90cf2-134">指令碼將會要求您提供 **principalName**的輸入。</span><span class="sxs-lookup"><span data-stu-id="90cf2-134">The script will ask you to provide an input for **principalName**.</span></span> <span data-ttu-id="90cf2-135">在此處提供您想要用來建立 Active Directory 應用程式 (例如 APIAuth) 的適當名稱。</span><span class="sxs-lookup"><span data-stu-id="90cf2-135">Provide a suitable name here that you want to use to create your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="90cf2-136">指令碼完成之後，它將會顯示下列四個值，您將需要以程式設計方式利用 AD 進行驗證，因此請確定會複製它們。</span><span class="sxs-lookup"><span data-stu-id="90cf2-136">After the script completes, it will display the following four values that you will need to authenticate programmatically with AD so make sure to copy them.</span></span> 
   
    <span data-ttu-id="90cf2-137">**TenantId**、**SubscriptionId**、**ApplicationId** 及 **Secret**。</span><span class="sxs-lookup"><span data-stu-id="90cf2-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="90cf2-138">您將使用 TenantId 做為 `{TENANT_ID}`、使用 ApplicationId 做為 `{CLIENT_ID}`，並使用 Secret 做為 `{CLIENT_SECRET}`。</span><span class="sxs-lookup"><span data-stu-id="90cf2-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="90cf2-139">預設的安全性原則可能會阻止您執行 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="90cf2-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="90cf2-140">如果是這樣，請使用下列命令，暫時設定您的執行原則來允許執行指令碼：</span><span class="sxs-lookup"><span data-stu-id="90cf2-140">If so, you temporarily configure your execution policy to allow script execution using the following command:</span></span>
   > 
   > <span data-ttu-id="90cf2-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="90cf2-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="90cf2-142">PS Cmdlet 組合看起來應如下所示。</span><span class="sxs-lookup"><span data-stu-id="90cf2-142">Here is how the set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="90cf2-143">查看 Azure 管理入口網站，會有一個新的 AD 應用程式是使用您提供給 [顯示我公司所擁有的應用程式] 下方名為 **principalName** 的指令碼的名稱所建立。</span><span class="sxs-lookup"><span data-stu-id="90cf2-143">Check in the Azure Management portal that a new AD application was created with the name you provided to the script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-to-get-a-valid-token"></a><span data-ttu-id="90cf2-144">取得有效權杖的步驟</span><span class="sxs-lookup"><span data-stu-id="90cf2-144">Steps to get a valid token</span></span>
1. <span data-ttu-id="90cf2-145">使用下列參數呼叫 API，且務必取代 TENANT\_ID、CLIENT\_ID 與 CLIENT\_SECRET：</span><span class="sxs-lookup"><span data-stu-id="90cf2-145">Call the API with the following parameters and make sure to replace the TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="90cf2-146">**要求 URL** 為 https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token</span><span class="sxs-lookup"><span data-stu-id="90cf2-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="90cf2-147">**HTTP Content-Type 標頭** 為 *application/x-www-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="90cf2-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="90cf2-148">**HTTP 要求主體**為 grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="90cf2-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="90cf2-149">以下是範例要求：</span><span class="sxs-lookup"><span data-stu-id="90cf2-149">The following is an example request:</span></span>
     
       <span data-ttu-id="90cf2-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="90cf2-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="90cf2-151">以下是範例回應：</span><span class="sxs-lookup"><span data-stu-id="90cf2-151">Here is an example response:</span></span>
     
       <span data-ttu-id="90cf2-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="90cf2-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="90cf2-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="90cf2-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="90cf2-154">這個範例包含 POST 參數的 URL 編碼，`resource` 值實際上是 `https://management.core.windows.net/`。</span><span class="sxs-lookup"><span data-stu-id="90cf2-154">This example included URL encoding of the POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="90cf2-155">請注意也要在 URL 中將 `{CLIENT_SECRET}` 編碼，因為它可能包含特殊字元。</span><span class="sxs-lookup"><span data-stu-id="90cf2-155">Be careful to also URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="90cf2-156">如需測試，您可以使用像是 [Fiddler](http://www.telerik.com/fiddler) 或 [Chrome Postman 擴充](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)的 HTTP 用戶端工具</span><span class="sxs-lookup"><span data-stu-id="90cf2-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="90cf2-157">現在，在每個 API 呼叫中加入授權要求標頭：</span><span class="sxs-lookup"><span data-stu-id="90cf2-157">Now in every API call, include the authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="90cf2-158">如果傳回 401 狀態碼，請檢查回應本文，其中可能指出權杖已過期。</span><span class="sxs-lookup"><span data-stu-id="90cf2-158">If you get a 401 status code returned, check the response body, it might tell you the token is expired.</span></span> <span data-ttu-id="90cf2-159">在此情況下，請取得新的權杖。</span><span class="sxs-lookup"><span data-stu-id="90cf2-159">In that case, get a new token.</span></span>

## <a name="using-the-apis"></a><span data-ttu-id="90cf2-160">使用 API</span><span class="sxs-lookup"><span data-stu-id="90cf2-160">Using the APIs</span></span>
<span data-ttu-id="90cf2-161">既然您已取得有效的權杖，您可以開始執行 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="90cf2-161">Now that you have a valid token, you are ready to make the API calls.</span></span>

1. <span data-ttu-id="90cf2-162">在每個 API 要求中，您必須傳遞您在上一節取得的有效、未過期的權杖。</span><span class="sxs-lookup"><span data-stu-id="90cf2-162">In each API request, you will need to pass a valid, unexpired token which you obtained in the previous section.</span></span>
2. <span data-ttu-id="90cf2-163">您需要在用來識別應用程式的要求 URI 中插入一些參數。</span><span class="sxs-lookup"><span data-stu-id="90cf2-163">You will need to plug in some parameters into the request URI which identifies your application.</span></span> <span data-ttu-id="90cf2-164">要求 URI 看起來如下所示</span><span class="sxs-lookup"><span data-stu-id="90cf2-164">The request URI looks like the following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="90cf2-165">若要取得參數，請按一下您的應用程式名稱，再按一下 [儀表板]，您將會看到如下的頁面和所有 3 個參數。</span><span class="sxs-lookup"><span data-stu-id="90cf2-165">To get the parameters, click on your application name and click Dashboard and you will see a page like the following with all the 3 parameters.</span></span>
   
   * <span data-ttu-id="90cf2-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="90cf2-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="90cf2-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="90cf2-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="90cf2-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="90cf2-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="90cf2-169">**4** 除非您建立一個新的，否則您的資源群組名稱應該是 **MobileEngagement**。</span><span class="sxs-lookup"><span data-stu-id="90cf2-169">**4** Your Resource Group name is going to be **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI 參數][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="90cf2-171">忽略 API 根位址，因為這適用於舊版 API。</span><span class="sxs-lookup"><span data-stu-id="90cf2-171">Ignore the API Root Address as this was for the previous APIs.</span></span><br/>
> 2. <span data-ttu-id="90cf2-172">若您已使用 Azure 傳統入口網站建立應用程式，則您就需要使用不同於應用程式名稱本身的應用程式資源名稱。</span><span class="sxs-lookup"><span data-stu-id="90cf2-172">If you created the app using Azure Classic portal then you need to use the Application Resource name which is different than the Application name itself.</span></span> <span data-ttu-id="90cf2-173">若您已在 Azure 入口網站內建立應用程式，則您應該使用應用程式其本身的名稱 (針對建立於新入口網站內的應用程式，在應用程式資源名稱與應用程式名稱之間其實並無差別)。</span><span class="sxs-lookup"><span data-stu-id="90cf2-173">If you created the app in the Azure Portal then you should use the App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in the new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



