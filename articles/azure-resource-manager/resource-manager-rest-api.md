---
title: "aaaResource 管理員 REST Api |Microsoft 文件"
description: "Hello 資源管理員 REST Api 驗證和使用方式範例的概觀"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="6e205-103">資源管理員 REST API</span><span class="sxs-lookup"><span data-stu-id="6e205-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e205-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e205-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="6e205-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6e205-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="6e205-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="6e205-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="6e205-107">REST API</span><span class="sxs-lookup"><span data-stu-id="6e205-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="6e205-108">每個已部署的範本，之後每個呼叫 tooAzure 資源管理員 中，後面背後的每個設定的儲存體帳戶有一或多個呼叫 toohello Azure 資源管理員的 RESTful API。</span><span class="sxs-lookup"><span data-stu-id="6e205-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="6e205-109">本主題是專供的 toothose Api 和如何呼叫它們而不使用任何 SDK。</span><span class="sxs-lookup"><span data-stu-id="6e205-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="6e205-110">如果您想要完整控制要求 tooAzure 或您慣用的語言 hello SDK 無法使用或不支援您所需要的 hello 操作，則這個方法會很有用。</span><span class="sxs-lookup"><span data-stu-id="6e205-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="6e205-111">這篇文章不會進出公開在 Azure 中，但而是使用某些作業做為範例的連接 toothem 的方式每一種 API。</span><span class="sxs-lookup"><span data-stu-id="6e205-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="6e205-112">了解 hello 基本概念之後，您可以閱讀 hello [Azure 資源管理員 REST API 參考](https://docs.microsoft.com/rest/api/resources/)toofind 的詳細資訊的 toouse hello rest hello 應用程式開發介面的方式。</span><span class="sxs-lookup"><span data-stu-id="6e205-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="6e205-113">驗證</span><span class="sxs-lookup"><span data-stu-id="6e205-113">Authentication</span></span>
<span data-ttu-id="6e205-114">Resource Manager 的驗證由 Azure Active Directory (AD) 處理。</span><span class="sxs-lookup"><span data-stu-id="6e205-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="6e205-115">tooconnect tooany API，您必須先 tooauthenticate 與 Azure AD tooreceive tooevery 要求，您可以傳遞之驗證語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6e205-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="6e205-116">因為我們要描述的純虛擬的呼叫，直接 toohello REST Api，我們假設您不想 tooauthenticate 由提示輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="6e205-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="6e205-117">我們也假設您不使用雙重要素驗證機制。</span><span class="sxs-lookup"><span data-stu-id="6e205-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="6e205-118">因此，我們會建立稱為 Azure AD 應用程式和服務主體所使用的 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="6e205-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="6e205-119">但是請記住，Azure AD 支援數項驗證程序和全部都可能是該驗證權杖，供後續的 API 要求所使用的 tooretrieve。</span><span class="sxs-lookup"><span data-stu-id="6e205-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="6e205-120">請依照[建立 Azure AD 應用程式和服務主體](resource-group-create-service-principal-portal.md)的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="6e205-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="6e205-121">產生存取權杖</span><span class="sxs-lookup"><span data-stu-id="6e205-121">Generating an Access Token</span></span>
<span data-ttu-id="6e205-122">Azure AD 的驗證方式是呼叫 tooAzure AD 中，位於 login.microsoftonline.com。tooauthenticate，您需要下列資訊 toohave hello:</span><span class="sxs-lookup"><span data-stu-id="6e205-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="6e205-123">Azure AD 租用戶識別碼 （hello Azure AD 使用 toolog 中的名稱，通常 hello 與您的公司相同但並非必要）</span><span class="sxs-lookup"><span data-stu-id="6e205-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="6e205-124">（已取得 hello Azure AD 應用程式建立步驟期間） 的應用程式識別碼</span><span class="sxs-lookup"><span data-stu-id="6e205-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="6e205-125">密碼 （您所選取建立 hello Azure AD 應用程式時）</span><span class="sxs-lookup"><span data-stu-id="6e205-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="6e205-126">在下列 HTTP 要求的 hello，請確定 tooreplace"Azure AD 租用戶識別碼"，"應用程式識別碼 」 和 「 密碼 」 及 hello 正確的值。</span><span class="sxs-lookup"><span data-stu-id="6e205-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="6e205-127">**一般 HTTP 要求︰**</span><span class="sxs-lookup"><span data-stu-id="6e205-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="6e205-128">...（如果驗證成功） 將導致回應類似 toohello 下列回應：</span><span class="sxs-lookup"><span data-stu-id="6e205-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
<span data-ttu-id="6e205-129">（在前面回應 hello hello access_token 已縮短的 tooincrease 可讀性）</span><span class="sxs-lookup"><span data-stu-id="6e205-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="6e205-130">**使用 Bash 產生存取權杖：**</span><span class="sxs-lookup"><span data-stu-id="6e205-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="6e205-131">**使用 PowerShell 產生存取權杖：**</span><span class="sxs-lookup"><span data-stu-id="6e205-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="6e205-132">hello 回應包含存取權杖、 資訊多久該語彙基元有效，以及相關資訊的資源，您可以使用該語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6e205-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="6e205-133">您在上一個 HTTP 呼叫 hello 中收到 hello 存取權杖必須傳入的所有要求 toohello 資源管理員 API。</span><span class="sxs-lookup"><span data-stu-id="6e205-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="6e205-134">您可以將它當做 hello 值"Bearer YOUR_ACCESS_TOKEN"名為 「 授權 」 標頭值。</span><span class="sxs-lookup"><span data-stu-id="6e205-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="6e205-135">請注意"Bearer"和存取權杖的 hello 間距。</span><span class="sxs-lookup"><span data-stu-id="6e205-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="6e205-136">您可以看到從 hello HTTP 結果上方，hello 權杖的有效期為特定的一段時間期間，您應該快取並重複使用該相同的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="6e205-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="6e205-137">即使是針對每個應用程式開發介面呼叫 Azure AD 可能 tooauthenticate，將高效率不佳。</span><span class="sxs-lookup"><span data-stu-id="6e205-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="6e205-138">呼叫 Resource Manager REST API</span><span class="sxs-lookup"><span data-stu-id="6e205-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="6e205-139">本主題只會使用幾個應用程式開發介面 tooexplain hello 基本用法的 hello REST 作業。</span><span class="sxs-lookup"><span data-stu-id="6e205-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="6e205-140">如需所有 hello 作業的資訊，請參閱[Azure 資源管理員 REST Api](https://docs.microsoft.com/rest/api/resources/)。</span><span class="sxs-lookup"><span data-stu-id="6e205-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="6e205-141">列出所有訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="6e205-141">List all subscriptions</span></span>
<span data-ttu-id="6e205-142">其中一個 hello 最簡單的作業，您可以為 toolist hello 可用訂用帳戶可以存取。</span><span class="sxs-lookup"><span data-stu-id="6e205-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="6e205-143">在 hello 下列要求，您會看到如何 hello 存取權杖以傳遞做為標頭：</span><span class="sxs-lookup"><span data-stu-id="6e205-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="6e205-144">(以您實際的存取權杖取代 YOUR_ACCESS_TOKEN。)</span><span class="sxs-lookup"><span data-stu-id="6e205-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="6e205-145">...，如此一來，您以取得訂用帳戶的清單，允許此服務主體 tooaccess</span><span class="sxs-lookup"><span data-stu-id="6e205-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="6e205-146">(為了便於閱讀，已縮短訂用帳戶識別碼)</span><span class="sxs-lookup"><span data-stu-id="6e205-146">(Subscription IDs have been shortened for readability)</span></span>

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="6e205-147">列出特定訂用帳戶中的所有資源群組</span><span class="sxs-lookup"><span data-stu-id="6e205-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="6e205-148">可用以 hello 資源管理員 Api 的所有資源都在資源群組巢都狀。</span><span class="sxs-lookup"><span data-stu-id="6e205-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="6e205-149">您可以使用下列 HTTP GET 要求的 hello 您訂用帳戶中現有的資源群組查詢資源管理員。</span><span class="sxs-lookup"><span data-stu-id="6e205-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="6e205-150">請注意如何 hello 訂用帳戶 ID 傳入 hello URL 的一部分此時間。</span><span class="sxs-lookup"><span data-stu-id="6e205-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="6e205-151">(以實際的存取權杖和訂用帳戶識別碼取代 YOUR_ACCESS_TOKEN 和 SUBSCRIPTION_ID)</span><span class="sxs-lookup"><span data-stu-id="6e205-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="6e205-152">hello 您收到的回應取決於您是否有定義任何資源群組，如果是這樣，多少。</span><span class="sxs-lookup"><span data-stu-id="6e205-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="6e205-153">(為了便於閱讀，已縮短訂用帳戶識別碼)</span><span class="sxs-lookup"><span data-stu-id="6e205-153">(Subscription IDs have been shortened for readability)</span></span>

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6e205-154">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="6e205-154">Create a resource group</span></span>
<span data-ttu-id="6e205-155">目前為止，我們已只被查詢 hello 資源管理員 Api 的資訊。</span><span class="sxs-lookup"><span data-stu-id="6e205-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="6e205-156">它是我們建立某些資源，並讓我們開始 hello 它們全部，資源群組的最簡單的時間。</span><span class="sxs-lookup"><span data-stu-id="6e205-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="6e205-157">hello 下列 HTTP 要求建立資源群組中 地區/您所選擇的位置，並將標記 tooit。</span><span class="sxs-lookup"><span data-stu-id="6e205-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="6e205-158">（取代 YOUR_ACCESS_TOKEN、 SUBSCRIPTION_ID、 RESOURCE_GROUP_NAME 您實際存取權杖、 訂用帳戶 ID 和名稱的 hello 想 toocreate 的資源群組）</span><span class="sxs-lookup"><span data-stu-id="6e205-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

<span data-ttu-id="6e205-159">如果成功，會產生下列回應類似 toohello 的回應：</span><span class="sxs-lookup"><span data-stu-id="6e205-159">If successful, you get a response that is similar toohello following response:</span></span>

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<span data-ttu-id="6e205-160">您已在 Azure 中成功建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="6e205-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="6e205-161">恭喜！</span><span class="sxs-lookup"><span data-stu-id="6e205-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="6e205-162">部署資源 tooa 資源群組使用資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="6e205-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="6e205-163">Resource Manager 可讓您使用範本來部署資源。</span><span class="sxs-lookup"><span data-stu-id="6e205-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="6e205-164">範本定義數個資源及其相依性。</span><span class="sxs-lookup"><span data-stu-id="6e205-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="6e205-165">本節中，我們假設您熟悉資源管理員範本和我們剛為您示範如何 toomake hello API 呼叫 toostart 部署。</span><span class="sxs-lookup"><span data-stu-id="6e205-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="6e205-166">如需有關建構範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="6e205-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6e205-167">部署範本不會與不同多 toohow 呼叫其他應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6e205-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="6e205-168">較特別的是部署範本可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="6e205-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="6e205-169">hello API 呼叫只會傳回，也可以 tooyou 為開發人員 tooquery 狀態為 hello 部署 toofind 出 hello 部署完成。</span><span class="sxs-lookup"><span data-stu-id="6e205-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="6e205-170">如需詳細資訊，請參閱[追蹤非同步 Azure 作業](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="6e205-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="6e205-171">在此範例中，我們使用 [GitHub](https://github.com/Azure/azure-quickstart-templates) 上提供的公開範本。</span><span class="sxs-lookup"><span data-stu-id="6e205-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="6e205-172">我們使用 hello 範本部署 Linux VM toohello 美國西部地區。</span><span class="sxs-lookup"><span data-stu-id="6e205-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="6e205-173">即使這個範例會使用公用等 GitHub 儲存機制中可用的範本，您可以改為傳遞 hello 完整範本，為 hello 要求的一部分。</span><span class="sxs-lookup"><span data-stu-id="6e205-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="6e205-174">請注意，我們提供了 hello 內所使用的參數值在 hello 要求部署範本。</span><span class="sxs-lookup"><span data-stu-id="6e205-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="6e205-175">（取代 SUBSCRIPTION_ID、 RESOURCE_GROUP_NAME、 DEPLOYMENT_NAME、 YOUR_ACCESS_TOKEN、 GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME、 ADMIN_USER_NAME、 ADMIN_PASSWORD 和 DNS_NAME_FOR_PUBLIC_IP toovalues 適用於您的要求）</span><span class="sxs-lookup"><span data-stu-id="6e205-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

<span data-ttu-id="6e205-176">hello 長 JSON 回應此要求已省略的 tooimprove 可讀性，這份文件。</span><span class="sxs-lookup"><span data-stu-id="6e205-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="6e205-177">hello 回應會包含您所建立的 hello 樣板化部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="6e205-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e205-178">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e205-178">Next steps</span></span>

- <span data-ttu-id="6e205-179">toolearn 有關處理非同步 REST 作業，請參閱[追蹤非同步的 Azure 作業](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="6e205-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
