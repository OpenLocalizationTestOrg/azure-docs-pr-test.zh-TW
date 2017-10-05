---
title: Resource Manager REST API | Microsoft Docs
description: "資源管理員 REST API 驗證和使用方式範例的概觀"
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
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="20d61-103">資源管理員 REST API</span><span class="sxs-lookup"><span data-stu-id="20d61-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="20d61-104">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20d61-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="20d61-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="20d61-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="20d61-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="20d61-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="20d61-107">REST API</span><span class="sxs-lookup"><span data-stu-id="20d61-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="20d61-108">在每次呼叫 Azure Resource Manager 時、每個部署的範本及每個設定的儲存體帳戶背後，都會呼叫 Azure Resource Manager 的 REST API 一次或多次。</span><span class="sxs-lookup"><span data-stu-id="20d61-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="20d61-109">本主題專門討論這些 API 以及如何在完全不使用任何 SDK 的情況下呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="20d61-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="20d61-110">如果您想要完全控制對 Azure 的要求、或您慣用的語言沒有適用的 SDK 或該 SDK 不支援您需要的作業，這種做法很有用。</span><span class="sxs-lookup"><span data-stu-id="20d61-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="20d61-111">本文並不會逐一介紹 Azure 中公開的每個 API，而是以某些 API 為例，說明如何連接至這些 API。</span><span class="sxs-lookup"><span data-stu-id="20d61-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="20d61-112">了解基本概念後，接著您可以閱讀 [Azure Resource Manager REST API 參考](https://docs.microsoft.com/rest/api/resources/)，找出如何使用其餘 API 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="20d61-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="20d61-113">驗證</span><span class="sxs-lookup"><span data-stu-id="20d61-113">Authentication</span></span>
<span data-ttu-id="20d61-114">Resource Manager 的驗證由 Azure Active Directory (AD) 處理。</span><span class="sxs-lookup"><span data-stu-id="20d61-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="20d61-115">若要連接至任何 API，您必須先向 Azure AD 進行驗證，以接收可以傳遞給每個要求的驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="20d61-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="20d61-116">因為我們要說明的是單純地呼叫直接 REST API，因此以您不想遵照提示輸入使用者名稱和密碼的假設來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="20d61-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="20d61-117">我們也假設您不使用雙重要素驗證機制。</span><span class="sxs-lookup"><span data-stu-id="20d61-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="20d61-118">因此，我們將建立用來登入的 Azure AD 應用程式和服務主體。</span><span class="sxs-lookup"><span data-stu-id="20d61-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="20d61-119">但請記住，Azure AD 支援數個驗證程序，而這些程序全都可以用來擷取後續 API 要求所需的驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="20d61-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="20d61-120">請依照[建立 Azure AD 應用程式和服務主體](resource-group-create-service-principal-portal.md)的逐步指示。</span><span class="sxs-lookup"><span data-stu-id="20d61-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="20d61-121">產生存取權杖</span><span class="sxs-lookup"><span data-stu-id="20d61-121">Generating an Access Token</span></span>
<span data-ttu-id="20d61-122">向外呼叫位於 login.microsoftonline.com 的 Azure AD，集合完成對 Azure AD 驗證。</span><span class="sxs-lookup"><span data-stu-id="20d61-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="20d61-123">若要驗證，您必須具有下列資訊︰</span><span class="sxs-lookup"><span data-stu-id="20d61-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="20d61-124">Azure AD 租用戶識別碼 (您用來登入的 Azure AD 名稱，通常與您的公司名稱相同，但不一定如此)</span><span class="sxs-lookup"><span data-stu-id="20d61-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="20d61-125">應用程式識別碼 (在 Azure AD 應用程式建立步驟期間取得)</span><span class="sxs-lookup"><span data-stu-id="20d61-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="20d61-126">密碼 (在建立 Azure AD 應用程式時選取）</span><span class="sxs-lookup"><span data-stu-id="20d61-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="20d61-127">在下列 HTTP 要求中，務必將 "Azure AD Tenant ID"、"Application ID" 和 "Password" 換成正確的值。</span><span class="sxs-lookup"><span data-stu-id="20d61-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="20d61-128">**一般 HTTP 要求︰**</span><span class="sxs-lookup"><span data-stu-id="20d61-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="20d61-129">... 將 (如果驗證成功) 產生類似下列的回應：</span><span class="sxs-lookup"><span data-stu-id="20d61-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

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
<span data-ttu-id="20d61-130">(已縮短先前回應中的 access_token，以提高可讀性)</span><span class="sxs-lookup"><span data-stu-id="20d61-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="20d61-131">**使用 Bash 產生存取權杖：**</span><span class="sxs-lookup"><span data-stu-id="20d61-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="20d61-132">**使用 PowerShell 產生存取權杖：**</span><span class="sxs-lookup"><span data-stu-id="20d61-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="20d61-133">此回應包含存取權杖、該權杖有效期間的相關資訊，以及您可以將該權杖用於哪項資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="20d61-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="20d61-134">您在先前 HTTP 呼叫中收到的存取權杖，必須傳給對 Resource Manager API 提出的所有要求。</span><span class="sxs-lookup"><span data-stu-id="20d61-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="20d61-135">您透過標頭值 "Authorization" 來傳遞它，值為 "Bearer YOUR_ACCESS_TOKEN"。</span><span class="sxs-lookup"><span data-stu-id="20d61-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="20d61-136">請注意 "Bearer" 與存取權杖之間的空格。</span><span class="sxs-lookup"><span data-stu-id="20d61-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="20d61-137">從上面的 HTTP 結果可以看出，權杖在一段特定時間內保持有效，您在這段期間內應該快取並重複使用該相同權杖。</span><span class="sxs-lookup"><span data-stu-id="20d61-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="20d61-138">即使可以對 Azure AD 進行每個 API 呼叫的驗證，但是會很沒效率。</span><span class="sxs-lookup"><span data-stu-id="20d61-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="20d61-139">呼叫 Resource Manager REST API</span><span class="sxs-lookup"><span data-stu-id="20d61-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="20d61-140">本主題只使用幾個 API 來說明 REST 作業的基本用法。</span><span class="sxs-lookup"><span data-stu-id="20d61-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="20d61-141">如需所有作業的相關資訊，請參閱 [Azure Resource Manager REST API](https://docs.microsoft.com/rest/api/resources/)。</span><span class="sxs-lookup"><span data-stu-id="20d61-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="20d61-142">列出所有訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="20d61-142">List all subscriptions</span></span>
<span data-ttu-id="20d61-143">您可以執行的最簡單作業之一，就是列出您可以存取的可用訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="20d61-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="20d61-144">在以下要求中，您會看到如何以標頭形式傳入存取權杖：</span><span class="sxs-lookup"><span data-stu-id="20d61-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="20d61-145">(以您實際的存取權杖取代 YOUR_ACCESS_TOKEN。)</span><span class="sxs-lookup"><span data-stu-id="20d61-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="20d61-146">...因此，您會取得允許此服務主體存取的訂用帳戶清單</span><span class="sxs-lookup"><span data-stu-id="20d61-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="20d61-147">(為了便於閱讀，已縮短訂用帳戶識別碼)</span><span class="sxs-lookup"><span data-stu-id="20d61-147">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="20d61-148">列出特定訂用帳戶中的所有資源群組</span><span class="sxs-lookup"><span data-stu-id="20d61-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="20d61-149">適用於 Resource Manager API 的所有資源都放在資源群組中。</span><span class="sxs-lookup"><span data-stu-id="20d61-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="20d61-150">您可以使用下列 HTTP GET 要求，向 Resource Manager 查詢訂用帳戶中的現有資源群組。</span><span class="sxs-lookup"><span data-stu-id="20d61-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="20d61-151">這次，請注意訂用帳戶識別碼如何作為 URL 的一部分而傳入。</span><span class="sxs-lookup"><span data-stu-id="20d61-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="20d61-152">(以實際的存取權杖和訂用帳戶識別碼取代 YOUR_ACCESS_TOKEN 和 SUBSCRIPTION_ID)</span><span class="sxs-lookup"><span data-stu-id="20d61-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="20d61-153">您收到的回應取決於是否已定義任何資源群組以及群組數量 (若已定義)。</span><span class="sxs-lookup"><span data-stu-id="20d61-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="20d61-154">(為了便於閱讀，已縮短訂用帳戶識別碼)</span><span class="sxs-lookup"><span data-stu-id="20d61-154">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="20d61-155">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="20d61-155">Create a resource group</span></span>
<span data-ttu-id="20d61-156">到目前為止，我們只向 Resource Manager API 查詢資訊。</span><span class="sxs-lookup"><span data-stu-id="20d61-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="20d61-157">現在該建立某些資源，讓我們從最簡單的開始，也就是資源群組。</span><span class="sxs-lookup"><span data-stu-id="20d61-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="20d61-158">下列 HTTP 要求會在您選擇的區域/位置建立資源群組，並新增它的標籤。</span><span class="sxs-lookup"><span data-stu-id="20d61-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="20d61-159">(以您實際的存取權杖、訂用帳戶識別碼和您要建立的資源群組名稱取代 YOUR_ACCESS_TOKEN、SUBSCRIPTION_ID、RESOURCE_GROUP_NAME)</span><span class="sxs-lookup"><span data-stu-id="20d61-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

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

<span data-ttu-id="20d61-160">如果成功，您會收到類似下列的回應：</span><span class="sxs-lookup"><span data-stu-id="20d61-160">If successful, you get a response that is similar to the following response:</span></span>

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

<span data-ttu-id="20d61-161">您已在 Azure 中成功建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="20d61-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="20d61-162">恭喜！</span><span class="sxs-lookup"><span data-stu-id="20d61-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="20d61-163">使用 Resource Manager 範本將資源部署至資源群組</span><span class="sxs-lookup"><span data-stu-id="20d61-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="20d61-164">Resource Manager 可讓您使用範本來部署資源。</span><span class="sxs-lookup"><span data-stu-id="20d61-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="20d61-165">範本定義數個資源及其相依性。</span><span class="sxs-lookup"><span data-stu-id="20d61-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="20d61-166">在本節中，我們假設您熟悉 Resource Manager 範本，我們只示範如何進行 API 呼叫以開始部署。</span><span class="sxs-lookup"><span data-stu-id="20d61-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="20d61-167">如需有關建構範本的詳細資訊，請參閱[編寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="20d61-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="20d61-168">部署範本和呼叫其他 API 沒有多大差異。</span><span class="sxs-lookup"><span data-stu-id="20d61-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="20d61-169">較特別的是部署範本可能需要很長的時間。</span><span class="sxs-lookup"><span data-stu-id="20d61-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="20d61-170">API 呼叫只是傳回資料，身為開發人員的您要負責查詢部署的狀態，以查明部署何時完成。</span><span class="sxs-lookup"><span data-stu-id="20d61-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="20d61-171">如需詳細資訊，請參閱[追蹤非同步 Azure 作業](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="20d61-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="20d61-172">在此範例中，我們使用 [GitHub](https://github.com/Azure/azure-quickstart-templates) 上提供的公開範本。</span><span class="sxs-lookup"><span data-stu-id="20d61-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="20d61-173">我們使用的範本會將 Linux VM 部署至美國西部區域。</span><span class="sxs-lookup"><span data-stu-id="20d61-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="20d61-174">雖然此範例使用 GitHub 等公開存放庫中提供的範本，您還是可以在要求中傳遞完整範本。</span><span class="sxs-lookup"><span data-stu-id="20d61-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="20d61-175">請注意，我們在要求中提供的參數值會用在部署的範本內。</span><span class="sxs-lookup"><span data-stu-id="20d61-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="20d61-176">(將 SUBSCRIPTION_ID、RESOURCE_GROUP_NAME、DEPLOYMENT_NAME、YOUR_ACCESS_TOKEN、GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME、ADMIN_USER_NAME、ADMIN_PASSWORD 和 DNS_NAME_FOR_PUBLIC_IP 換成適合要求的值)</span><span class="sxs-lookup"><span data-stu-id="20d61-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

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

<span data-ttu-id="20d61-177">為了提高本文件的可讀性，已省略此要求較長的 JSON 回應。</span><span class="sxs-lookup"><span data-stu-id="20d61-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="20d61-178">回應會包含您建立之樣板化部署的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="20d61-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20d61-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="20d61-179">Next steps</span></span>

- <span data-ttu-id="20d61-180">若要了解處理非同步 REST 作業，請參閱[追蹤非同步 Azure 作業](resource-manager-async-operations.md)。</span><span class="sxs-lookup"><span data-stu-id="20d61-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
