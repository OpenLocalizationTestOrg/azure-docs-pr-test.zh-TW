---
title: "aaaAzure 事件方格安全性和驗證"
description: "說明 Azure Event Grid 與其概念。"
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="fb065-103">Event Grid 安全性與驗證</span><span class="sxs-lookup"><span data-stu-id="fb065-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="fb065-104">Azure Event Grid 有三種驗證方法：</span><span class="sxs-lookup"><span data-stu-id="fb065-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="fb065-105">事件訂閱</span><span class="sxs-lookup"><span data-stu-id="fb065-105">Event subscriptions</span></span>
* <span data-ttu-id="fb065-106">事件發佈</span><span class="sxs-lookup"><span data-stu-id="fb065-106">Event publishing</span></span>
* <span data-ttu-id="fb065-107">WebHook 事件傳遞</span><span class="sxs-lookup"><span data-stu-id="fb065-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="fb065-108">WebHook 事件傳遞</span><span class="sxs-lookup"><span data-stu-id="fb065-108">WebHook Event delivery</span></span>

<span data-ttu-id="fb065-109">Webhook 為其中一個即時 Azure 事件方格中的許多方式 tooreceive 事件。</span><span class="sxs-lookup"><span data-stu-id="fb065-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="fb065-110">每當有未傳遞新事件準備 toobe，事件方格會傳送 HTTP 要求與 hello 事件 tooyour WebHook 與 hello 主體中。</span><span class="sxs-lookup"><span data-stu-id="fb065-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="fb065-111">當您註冊您自己的 WebHook 端點事件方格時，它傳送給您以簡單的驗證程式碼的 POST 要求中順序 tooprove 端點擁有權。</span><span class="sxs-lookup"><span data-stu-id="fb065-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="fb065-112">您的應用程式需要 toorespond 回應後 hello 驗證程式碼。</span><span class="sxs-lookup"><span data-stu-id="fb065-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="fb065-113">事件方格將不會傳送事件 tooWebHook 皆未通過 hello 驗證的端點。</span><span class="sxs-lookup"><span data-stu-id="fb065-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="fb065-114">驗證詳細資料：</span><span class="sxs-lookup"><span data-stu-id="fb065-114">Validation details:</span></span>

* <span data-ttu-id="fb065-115">在 hello 訂用帳戶建立/更新事件時，事件方格會公佈"SubscriptionValidationEvent 」 事件 toohello 目標端點。</span><span class="sxs-lookup"><span data-stu-id="fb065-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="fb065-116">hello 事件中包含的標頭值 「 事件類型:: 驗證 」。</span><span class="sxs-lookup"><span data-stu-id="fb065-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="fb065-117">hello 事件主體具有 hello 和其他事件方格事件相同的結構描述。</span><span class="sxs-lookup"><span data-stu-id="fb065-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="fb065-118">hello 事件資料包含以隨機產生的字串"ValidationCode"屬性例如“ValidationCode: acb13…”。</span><span class="sxs-lookup"><span data-stu-id="fb065-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="fb065-119">順序 tooprove 端點擁有權，以回應後 hello 驗證程式碼如"ValidationResponse: acb13...」。</span><span class="sxs-lookup"><span data-stu-id="fb065-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="fb065-120">最後，它是重要 toonote Azure 事件方格僅支援 HTTPS webhook 端點。</span><span class="sxs-lookup"><span data-stu-id="fb065-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="fb065-121">事件訂閱</span><span class="sxs-lookup"><span data-stu-id="fb065-121">Event subscription</span></span>

<span data-ttu-id="fb065-122">toosubscribe tooan 事件，您必須擁有 hello **Microsoft.EventGrid/EventSubscriptions/Write** hello 權限所需的資源。</span><span class="sxs-lookup"><span data-stu-id="fb065-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="fb065-123">您需要此權限，因為您要撰寫的新訂用帳戶在 hello 範圍 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="fb065-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="fb065-124">hello 必要資源與根據您要訂閱 tooa 系統主題或自訂的主題。</span><span class="sxs-lookup"><span data-stu-id="fb065-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="fb065-125">本節會說明這兩種類型。</span><span class="sxs-lookup"><span data-stu-id="fb065-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="fb065-126">系統主題 (Azure 服務發行者)</span><span class="sxs-lookup"><span data-stu-id="fb065-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="fb065-127">對於系統的主題，您需要權限 toowrite 新事件訂閱 hello 範圍的 hello 資源發佈 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="fb065-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="fb065-128">hello hello 之資源的格式如下：`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="fb065-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="fb065-129">例如，toosubscribe tooan 事件上名為的儲存體帳戶**myacct**，您在需要 hello Microsoft.EventGrid/EventSubscriptions/Write 權限：`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="fb065-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="fb065-130">自訂主題</span><span class="sxs-lookup"><span data-stu-id="fb065-130">Custom topics</span></span>

<span data-ttu-id="fb065-131">如需自訂主題，您需要權限 toowrite 新事件訂閱 hello 範圍的 hello 事件方格主題。</span><span class="sxs-lookup"><span data-stu-id="fb065-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="fb065-132">hello hello 之資源的格式如下：`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="fb065-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="fb065-133">例如，toosubscribe tooa 自訂主題名為**mytopic**，您在需要 hello Microsoft.EventGrid/EventSubscriptions/Write 權限：`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="fb065-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="fb065-134">主題發佈</span><span class="sxs-lookup"><span data-stu-id="fb065-134">Topic publishing</span></span>

<span data-ttu-id="fb065-135">主題使用共用存取簽章 (SAS) 或金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="fb065-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="fb065-136">我們建議使用 SAS，但金鑰驗證提供簡單的程式編寫，並且與許多現有的 Webhook 發佈者相容。</span><span class="sxs-lookup"><span data-stu-id="fb065-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="fb065-137">Hello HTTP 標頭中包含 hello 驗證值。</span><span class="sxs-lookup"><span data-stu-id="fb065-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="fb065-138">使用 SAS， **aeg sas 權杖**hello 標頭值。</span><span class="sxs-lookup"><span data-stu-id="fb065-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="fb065-139">針對驗證、 使用**aeg sas 金鑰**hello 標頭值。</span><span class="sxs-lookup"><span data-stu-id="fb065-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="fb065-140">金鑰驗證</span><span class="sxs-lookup"><span data-stu-id="fb065-140">Key authentication</span></span>

<span data-ttu-id="fb065-141">Hello 最簡單形式的驗證金鑰驗證。</span><span class="sxs-lookup"><span data-stu-id="fb065-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="fb065-142">使用 hello 格式：`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="fb065-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="fb065-143">舉例來說，您將金鑰與此一起傳遞：</span><span class="sxs-lookup"><span data-stu-id="fb065-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="fb065-144">SAS 權杖</span><span class="sxs-lookup"><span data-stu-id="fb065-144">SAS tokens</span></span>

<span data-ttu-id="fb065-145">事件方格的 SAS 權杖包含 hello 資源、 到期時間和簽章。</span><span class="sxs-lookup"><span data-stu-id="fb065-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="fb065-146">hello hello SAS 權杖的格式為： `r={resource}&e={expiration}&s={signature}`。</span><span class="sxs-lookup"><span data-stu-id="fb065-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="fb065-147">hello 資源是 hello 路徑的 hello 主題 toowhich 傳送事件。</span><span class="sxs-lookup"><span data-stu-id="fb065-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="fb065-148">以下為一個有效資源路徑的例子：`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="fb065-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="fb065-149">您可以產生 hello 簽章從機碼。</span><span class="sxs-lookup"><span data-stu-id="fb065-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="fb065-150">以下為一個有效 **aeg-sas-token** 值的例子：</span><span class="sxs-lookup"><span data-stu-id="fb065-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="fb065-151">hello 下列範例會建立 SAS 權杖使用事件方格：</span><span class="sxs-lookup"><span data-stu-id="fb065-151">hello following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="fb065-152">Management Access Control</span><span class="sxs-lookup"><span data-stu-id="fb065-152">Management Access Control</span></span>

<span data-ttu-id="fb065-153">Azure 事件方格可讓您 toocontrol hello 的層級指定的存取 toodifferent 使用者 toodo 各種管理操作，例如清單事件訂閱、 建立新的並產生索引鍵。</span><span class="sxs-lookup"><span data-stu-id="fb065-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="fb065-154">Event Grid 為此使用 Azure 的 Role Based Access Check (RBAC)。</span><span class="sxs-lookup"><span data-stu-id="fb065-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="fb065-155">作業類型</span><span class="sxs-lookup"><span data-stu-id="fb065-155">Operation types</span></span>

<span data-ttu-id="fb065-156">Azure 事件方格支援 hello 下列動作：</span><span class="sxs-lookup"><span data-stu-id="fb065-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="fb065-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="fb065-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="fb065-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="fb065-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="fb065-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="fb065-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="fb065-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="fb065-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="fb065-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="fb065-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="fb065-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="fb065-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="fb065-163">hello 最後三個作業傳回潛在機密資訊的取得從標準的讀取作業中篩選掉。</span><span class="sxs-lookup"><span data-stu-id="fb065-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="fb065-164">為您 toorestrict 存取 toothese 作業的最佳作法是。</span><span class="sxs-lookup"><span data-stu-id="fb065-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="fb065-165">您可以使用建立自訂角色[Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)， [Azure 命令列介面 (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md)，和 hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md)。</span><span class="sxs-lookup"><span data-stu-id="fb065-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="fb065-166">強制執行 Role Based Access Check (RBAC)</span><span class="sxs-lookup"><span data-stu-id="fb065-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="fb065-167">使用下列步驟 tooenforce RBAC 針對不同使用者的 hello:</span><span class="sxs-lookup"><span data-stu-id="fb065-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="fb065-168">建立自訂的角色定義檔案 (.json)</span><span class="sxs-lookup"><span data-stu-id="fb065-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="fb065-169">hello 下面是範例事件方格角色定義可讓使用者 tooperform 組不同的動作。</span><span class="sxs-lookup"><span data-stu-id="fb065-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="fb065-170">**EventGridReadOnlyRole.json**：只允許唯讀作業。</span><span class="sxs-lookup"><span data-stu-id="fb065-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="fb065-171">**EventGridNoDeleteListKeysRole.json**：允許限制的張貼動作，但不允許刪除。</span><span class="sxs-lookup"><span data-stu-id="fb065-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="fb065-172">**EventGridContributorRole.json**：允許所有 Grid 動作。</span><span class="sxs-lookup"><span data-stu-id="fb065-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="fb065-173">安裝與登入 tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="fb065-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="fb065-174">Azure CLI 0.8.8 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="fb065-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="fb065-175">tooinstall hello 最新版本並關聯它與您 Azure 訂用帳戶，請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="fb065-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="fb065-176">Azure CLI 中的 Azure Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="fb065-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="fb065-177">跳過[hello 資源管理員的使用 hello Azure CLI](../xplat-cli-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="fb065-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="fb065-178">建立自訂角色</span><span class="sxs-lookup"><span data-stu-id="fb065-178">Create a custom role</span></span>

<span data-ttu-id="fb065-179">toocreate 自訂安全性角色，使用：</span><span class="sxs-lookup"><span data-stu-id="fb065-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="fb065-180">Hello 角色 tooa 使用者指派</span><span class="sxs-lookup"><span data-stu-id="fb065-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="fb065-181">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb065-181">Next steps</span></span>

* <span data-ttu-id="fb065-182">如簡介 tooEvent 格線，請參閱[有關事件方格](overview.md)</span><span class="sxs-lookup"><span data-stu-id="fb065-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>
