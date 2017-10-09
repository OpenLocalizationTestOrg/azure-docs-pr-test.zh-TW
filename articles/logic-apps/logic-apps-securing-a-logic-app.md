---
title: "aaaSecure 存取 tooAzure Logic Apps |Microsoft 文件"
description: "新增安全性來保護存取 tootriggers、 輸入和輸出、 動作參數，以及與 Azure 邏輯應用程式中的工作流程搭配使用的服務。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="f4fea-103">安全存取 tooyour 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="f4fea-104">有許多工具可用 toohelp 安全應用程式邏輯。</span><span class="sxs-lookup"><span data-stu-id="f4fea-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="f4fea-105">保護存取 tootrigger 邏輯應用程式 （HTTP 要求觸發程序）</span><span class="sxs-lookup"><span data-stu-id="f4fea-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="f4fea-106">保護存取 toomanage 編輯或讀取邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="f4fea-107">保護存取 toocontents 的測試回合的輸入和輸出</span><span class="sxs-lookup"><span data-stu-id="f4fea-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="f4fea-108">保護工作流程中動作內的參數或輸入</span><span class="sxs-lookup"><span data-stu-id="f4fea-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="f4fea-109">從工作流程中接收要求的安全存取 tooservices</span><span class="sxs-lookup"><span data-stu-id="f4fea-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="f4fea-110">安全存取 tootrigger</span><span class="sxs-lookup"><span data-stu-id="f4fea-110">Secure access tootrigger</span></span>

<span data-ttu-id="f4fea-111">當您使用邏輯應用程式引發 HTTP 要求 ([要求](../connectors/connectors-native-reqres.md)或[Webhook](../connectors/connectors-native-webhook.md))，您可以限制存取，讓只有獲得授權的用戶端可以引發 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fea-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="f4fea-112">所有傳入邏輯應用程式的要求都會透過 SSL 加密並保護。</span><span class="sxs-lookup"><span data-stu-id="f4fea-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="f4fea-113">共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="f4fea-113">Shared Access Signature</span></span>

<span data-ttu-id="f4fea-114">邏輯應用程式的每個要求端點包含[共用存取簽章 (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="f4fea-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="f4fea-115">每個 URL 都包含 `sp`、`sv` 和 `sig` 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="f4fea-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="f4fea-116">所指定權限`sp`，而且對應 tooHTTP 方法允許，`sv`是 hello 使用版本 toogenerate，和`sig`是使用的 tooauthenticate 存取 tootrigger。</span><span class="sxs-lookup"><span data-stu-id="f4fea-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="f4fea-117">hello 簽章會產生與秘密金鑰的所有 hello URL 路徑和屬性上使用 hello SHA256 演算法。</span><span class="sxs-lookup"><span data-stu-id="f4fea-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="f4fea-118">hello 祕密金鑰永遠不會公開和發行，並會保留加密並儲存，一部分的 hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fea-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="f4fea-119">邏輯應用程式只會授權包含有效的簽章與 hello 祕密金鑰建立的觸發程序。</span><span class="sxs-lookup"><span data-stu-id="f4fea-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="f4fea-120">重新產生存取金鑰</span><span class="sxs-lookup"><span data-stu-id="f4fea-120">Regenerate access keys</span></span>

<span data-ttu-id="f4fea-121">您可以重新產生新的安全金鑰在任何時候透過 hello REST API 或 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="f4fea-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="f4fea-122">先前使用 hello 舊金鑰產生的所有目前 Url 會失效，無法再授權 toofire hello 邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fea-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="f4fea-123">在 hello Azure 入口網站，開啟您想 tooregenerate 索引鍵的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="f4fea-124">按一下 hello**便捷鍵**下的功能表項目**設定**</span><span class="sxs-lookup"><span data-stu-id="f4fea-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="f4fea-125">選擇 hello 金鑰 tooregenerate 和完整 hello 程序</span><span class="sxs-lookup"><span data-stu-id="f4fea-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="f4fea-126">您重新產生之後擷取的 Url 會以 hello 新的存取金鑰簽署。</span><span class="sxs-lookup"><span data-stu-id="f4fea-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="f4fea-127">使用具有到期日期的回呼 URL</span><span class="sxs-lookup"><span data-stu-id="f4fea-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="f4fea-128">如果您與其他合作對象共用 hello URL，您可以在具有特定索引鍵和到期日，視需要產生 Url。</span><span class="sxs-lookup"><span data-stu-id="f4fea-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="f4fea-129">您可以順暢地向前復原索引鍵，或確定存取 toofire 應用程式是受限制的 tooa 特定 timespan。</span><span class="sxs-lookup"><span data-stu-id="f4fea-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="f4fea-130">您可以指定到期日 hello 透過 url [REST API 的 logic apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="f4fea-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="f4fea-131">Hello 主體中包含 hello 屬性`NotAfter`為 JSON 的日期字串，它會傳回回呼 URL，才會有效直到 hello`NotAfter`日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f4fea-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="f4fea-132">建立具有主要或次要秘密金鑰的 URL</span><span class="sxs-lookup"><span data-stu-id="f4fea-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="f4fea-133">當您產生，或以要求為基礎的觸發程序的回呼 Url 的清單時，您也可以指定哪些金鑰 toouse toosign hello URL。</span><span class="sxs-lookup"><span data-stu-id="f4fea-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="f4fea-134">您可以產生 URL，由 hello 透過特定的金鑰簽署[REST API 的 logic apps](https://docs.microsoft.com/rest/api/logic/workflowtriggers) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f4fea-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="f4fea-135">Hello 主體中包含 hello 屬性`KeyType`為`Primary`或`Secondary`。</span><span class="sxs-lookup"><span data-stu-id="f4fea-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="f4fea-136">這會傳回所指定的 hello 安全金鑰簽章的 URL。</span><span class="sxs-lookup"><span data-stu-id="f4fea-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="f4fea-137">限制傳入的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f4fea-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="f4fea-138">此外 toohello 共用存取簽章，您可能想要 toorestrict 只從特定的用戶端呼叫邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fea-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="f4fea-139">例如，如果您管理您的端點，透過 Azure API 管理，您可以限制 hello 邏輯應用程式 tooonly 接受 hello 要求，當 hello 要求來自 hello API 管理執行個體的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f4fea-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="f4fea-140">可以在 hello 邏輯應用程式設定中設定此設定：</span><span class="sxs-lookup"><span data-stu-id="f4fea-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="f4fea-141">在 hello Azure 入口網站，開啟您想 tooadd IP 位址限制的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="f4fea-142">按一下 hello**存取控制設定**下的功能表項目**設定**</span><span class="sxs-lookup"><span data-stu-id="f4fea-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="f4fea-143">指定 IP 位址範圍 toobe hello 觸發程序所接受的 hello 的清單</span><span class="sxs-lookup"><span data-stu-id="f4fea-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="f4fea-144">有效的 IP 範圍可接受 hello 格式`192.168.1.1/255`。</span><span class="sxs-lookup"><span data-stu-id="f4fea-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="f4fea-145">如果您想 hello 邏輯應用程式 tooonly 引發為巢狀的邏輯應用程式，請選取 hello**只有其他的 logic apps**選項。</span><span class="sxs-lookup"><span data-stu-id="f4fea-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="f4fea-146">此選項會將空的陣列 toohello 資源，這表示只有呼叫 hello 從服務本身 （父邏輯應用程式） 引發已成功。</span><span class="sxs-lookup"><span data-stu-id="f4fea-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="f4fea-147">您仍然可以執行要求的觸發程序邏輯應用程式，透過 REST API hello / 管理`/triggers/{triggerName}/run`不論 IP。</span><span class="sxs-lookup"><span data-stu-id="f4fea-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="f4fea-148">此案例需要驗證的 hello Azure REST API，而且所有事件會都出現在 hello Azure 稽核記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f4fea-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="f4fea-149">請適當地設定存取控制原則。</span><span class="sxs-lookup"><span data-stu-id="f4fea-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="f4fea-150">在 hello 資源定義上設定 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="f4fea-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="f4fea-151">如果您使用[部署範本](logic-apps-create-deploy-template.md)tooautomate 可以 hello 資源範本設定您的部署 hello IP 範圍設定。</span><span class="sxs-lookup"><span data-stu-id="f4fea-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="f4fea-152">新增 Azure Active Directory、OAuth 或其他安全性</span><span class="sxs-lookup"><span data-stu-id="f4fea-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="f4fea-153">更多授權通訊協定在邏輯應用程式頂端的 tooadd [Azure API 管理](https://azure.microsoft.com/services/api-management/)當做 API 邏輯應用程式提供豐富監視、 安全性、 原則和文件以 hello 功能 tooexpose 任何端點。</span><span class="sxs-lookup"><span data-stu-id="f4fea-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="f4fea-154">Azure API 管理可以公開 hello 邏輯應用程式，這可以使用 Azure Active Directory、 憑證、 OAuth、 或其他安全性標準的公用或私用端點。</span><span class="sxs-lookup"><span data-stu-id="f4fea-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="f4fea-155">收到要求時，Azure API 管理轉送 hello 要求 toohello 邏輯應用程式 （執行任何所需的轉換或進行中的限制）。</span><span class="sxs-lookup"><span data-stu-id="f4fea-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="f4fea-156">您可以使用 hello hello 邏輯應用程式 tooonly 上的設定允許 hello 邏輯應用程式 toobe 觸發從 API 管理連入 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="f4fea-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="f4fea-157">安全存取 toomanage 或編輯邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="f4fea-158">您可以限制存取 toomanagement 作業邏輯應用程式，以便只有特定使用者或群組能夠 tooperform hello 資源上的作業。</span><span class="sxs-lookup"><span data-stu-id="f4fea-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="f4fea-159">邏輯應用程式使用 hello Azure[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md)功能，並且可以自訂以 hello 相同的工具。</span><span class="sxs-lookup"><span data-stu-id="f4fea-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="f4fea-160">有幾個內建的角色，您也可以將指派的訂用帳戶 tooas 成員：</span><span class="sxs-lookup"><span data-stu-id="f4fea-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="f4fea-161">**邏輯應用程式參與者**-提供存取 tooview、 編輯和更新邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fea-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="f4fea-162">無法移除 hello 資源或執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="f4fea-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="f4fea-163">**邏輯應用程式運算子**-可以檢視 hello 邏輯應用程式和執行歷程記錄，並啟用/停用。</span><span class="sxs-lookup"><span data-stu-id="f4fea-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="f4fea-164">無法編輯或更新 hello 定義。</span><span class="sxs-lookup"><span data-stu-id="f4fea-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="f4fea-165">您也可以使用[Azure 資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)tooprevent 變更或刪除邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="f4fea-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="f4fea-166">此功能相當重要 tooprevent 實際執行資源變更或刪除。</span><span class="sxs-lookup"><span data-stu-id="f4fea-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="f4fea-167">安全存取 toocontents 的 hello 執行歷程記錄</span><span class="sxs-lookup"><span data-stu-id="f4fea-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="f4fea-168">您可以從上一個回合 toospecific IP 位址範圍來限制存取 toocontents 的輸入或輸出。</span><span class="sxs-lookup"><span data-stu-id="f4fea-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="f4fea-169">工作流程執行中的所有資料在傳輸及靜止時都會加密。</span><span class="sxs-lookup"><span data-stu-id="f4fea-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="f4fea-170">當呼叫 toorun 記錄時，hello 服務驗證 hello 要求，並提供連結 toohello 要求和回應輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="f4fea-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="f4fea-171">這個連結可以在受保護的只要求指定的 IP 位址範圍內的 tooview 內容傳回 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="f4fea-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="f4fea-172">您可以使用此功能來進行其他存取控制。</span><span class="sxs-lookup"><span data-stu-id="f4fea-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="f4fea-173">您甚至可以指定如 `0.0.0.0` 的 IP 位址，這樣就沒有人可以存取輸入/輸出。</span><span class="sxs-lookup"><span data-stu-id="f4fea-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="f4fea-174">只有具備系統管理員權限的人可能會移除這項限制，提供 hello 可能性 '在 just-in-time' 存取 tooworkflow 內容。</span><span class="sxs-lookup"><span data-stu-id="f4fea-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="f4fea-175">中的 hello Azure 入口網站的 hello 資源設定，可以設定此設定：</span><span class="sxs-lookup"><span data-stu-id="f4fea-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="f4fea-176">在 hello Azure 入口網站，開啟您想 tooadd IP 位址限制的 hello 邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="f4fea-177">按一下 hello**存取控制設定**下的功能表項目**設定**</span><span class="sxs-lookup"><span data-stu-id="f4fea-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="f4fea-178">指定 IP 位址範圍存取 toocontent hello 的清單</span><span class="sxs-lookup"><span data-stu-id="f4fea-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="f4fea-179">在 hello 資源定義上設定 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="f4fea-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="f4fea-180">如果您使用[部署範本](logic-apps-create-deploy-template.md)tooautomate 可以 hello 資源範本設定您的部署 hello IP 範圍設定。</span><span class="sxs-lookup"><span data-stu-id="f4fea-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="f4fea-181">保護工作流程中的參數和輸入</span><span class="sxs-lookup"><span data-stu-id="f4fea-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="f4fea-182">您可以 tooparameterize 部署的工作流程定義的某些層面的環境。</span><span class="sxs-lookup"><span data-stu-id="f4fea-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="f4fea-183">此外，某些參數可能是安全的參數，編輯工作流程，例如用戶端識別碼和用戶端密碼時，您不想 tooappear [Azure Active Directory 驗證](../connectors/connectors-native-http.md#authentication)的 HTTP 動作。</span><span class="sxs-lookup"><span data-stu-id="f4fea-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="f4fea-184">使用參數和安全參數</span><span class="sxs-lookup"><span data-stu-id="f4fea-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="f4fea-185">tooaccess hello 資源在執行階段，參數值的 hello[工作流程定義語言](http://aka.ms/logicappsdocs)提供`@parameters()`作業。</span><span class="sxs-lookup"><span data-stu-id="f4fea-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="f4fea-186">此外，您也可以[hello 資源部署範本中指定參數](../azure-resource-manager/resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="f4fea-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="f4fea-187">但是，如果您指定 hello 參數類型為`securestring`，hello 參數將不會傳回與 hello 其餘 hello 資源定義，而且不會藉由部署後檢視 hello 資源存取。</span><span class="sxs-lookup"><span data-stu-id="f4fea-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="f4fea-188">如果您的參數使用 hello 標頭或要求主體中，hello 參數可能會看到存取 hello 執行歷程記錄和外送 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="f4fea-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="f4fea-189">因此請確定 tooset 內容的存取原則。</span><span class="sxs-lookup"><span data-stu-id="f4fea-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="f4fea-190">授權標頭絕對不會透過輸入或輸出來顯示。</span><span class="sxs-lookup"><span data-stu-id="f4fea-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="f4fea-191">因此如果有使用 hello 密碼，hello 密碼不可以擷取。</span><span class="sxs-lookup"><span data-stu-id="f4fea-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="f4fea-192">含有密碼的資源部署範本</span><span class="sxs-lookup"><span data-stu-id="f4fea-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="f4fea-193">hello 下列範例將示範參考參數的安全部署`secret`在執行階段。</span><span class="sxs-lookup"><span data-stu-id="f4fea-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="f4fea-194">在不同的參數檔案中，您可以指定 hello 的 hello 環境值`secret`，或使用[Azure 資源管理員 KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve 機密資料，在部署階段。</span><span class="sxs-lookup"><span data-stu-id="f4fea-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="f4fea-195">安全存取 tooservices 接收要求，從工作流程</span><span class="sxs-lookup"><span data-stu-id="f4fea-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="f4fea-196">有許多方式 toohelp 安全任何端點 hello 邏輯應用程式需要 tooaccess。</span><span class="sxs-lookup"><span data-stu-id="f4fea-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="f4fea-197">在外送要求上使用驗證</span><span class="sxs-lookup"><span data-stu-id="f4fea-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="f4fea-198">當使用 HTTP、 HTTP + Swagger (開啟的 API) 或 Webhook 動作，您可以加入驗證 toohello 要求傳送。</span><span class="sxs-lookup"><span data-stu-id="f4fea-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="f4fea-199">您可以包括基本驗證、憑證驗證或 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="f4fea-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="f4fea-200">有關如何 tooconfigure 此驗證可找到[本文](../connectors/connectors-native-http.md#authentication)。</span><span class="sxs-lookup"><span data-stu-id="f4fea-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="f4fea-201">限制存取 toologic 應用程式的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="f4fea-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="f4fea-202">邏輯應用程式的所有呼叫都來自每個區域一組特定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f4fea-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="f4fea-203">您可以加入其他篩選 tooonly 接受來自指定 IP 位址的要求。</span><span class="sxs-lookup"><span data-stu-id="f4fea-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="f4fea-204">如需這些 IP 位址清單，請參閱[邏輯應用程式的限制和設定](logic-apps-limits-and-config.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="f4fea-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="f4fea-205">內部部署連線能力</span><span class="sxs-lookup"><span data-stu-id="f4fea-205">On-premises connectivity</span></span>

<span data-ttu-id="f4fea-206">邏輯應用程式提供數個服務 tooprovide 安全、 可靠與整合的內部通訊。</span><span class="sxs-lookup"><span data-stu-id="f4fea-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="f4fea-207">內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="f4fea-207">On-premises data gateway</span></span>

<span data-ttu-id="f4fea-208">多 managed 的連接器邏輯應用程式提供安全的連線 tooon 內部部署系統，包括檔案系統、 SQL、 SharePoint、 DB2 和更多。</span><span class="sxs-lookup"><span data-stu-id="f4fea-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="f4fea-209">hello 閘道轉送上 hello Azure Service Bus 透過加密通道在內部部署來源的資料。</span><span class="sxs-lookup"><span data-stu-id="f4fea-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="f4fea-210">所有流量都來自為 hello 閘道代理程式的安全輸出流量。</span><span class="sxs-lookup"><span data-stu-id="f4fea-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="f4fea-211">深入了解[hello 資料閘道的運作方式](logic-apps-gateway-install.md#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="f4fea-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="f4fea-212">Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="f4fea-212">Azure API Management</span></span>

<span data-ttu-id="f4fea-213">[Azure API 管理](https://azure.microsoft.com/services/api-management/)有內部部署連線選項，包括安全的 proxy 和通訊 tooon 內部部署系統的站對站 VPN 和 ExpressRoute 整合。</span><span class="sxs-lookup"><span data-stu-id="f4fea-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="f4fea-214">在 hello 邏輯應用程式的設計工具，您可以快速地選取 API 從 Azure API 管理公開工作流程中，提供快速存取 tooon 內部部署系統。</span><span class="sxs-lookup"><span data-stu-id="f4fea-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="f4fea-215">Azure App Service 的混合式連線</span><span class="sxs-lookup"><span data-stu-id="f4fea-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="f4fea-216">Azure API 和 Web 應用程式 toocommunicate 內部部署，您可以使用 hello 在內部部署混合式連接功能。</span><span class="sxs-lookup"><span data-stu-id="f4fea-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="f4fea-217">混合式連線及 tooconfigure 可以找到方式的詳細資訊[本文](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f4fea-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4fea-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4fea-218">Next steps</span></span>
[<span data-ttu-id="f4fea-219">建立部署範本</span><span class="sxs-lookup"><span data-stu-id="f4fea-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="f4fea-220">例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="f4fea-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="f4fea-221">監視邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="f4fea-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="f4fea-222">診斷邏輯應用程式失敗和問題</span><span class="sxs-lookup"><span data-stu-id="f4fea-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
