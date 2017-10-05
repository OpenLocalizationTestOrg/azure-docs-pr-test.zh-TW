---
title: "安全存取 Azure Logic Apps | Microsoft Docs"
description: "新增安全性以保護存取 Azure Logic Apps 中工作流程使用的觸發程序、輸入和輸出、動作參數和服務。"
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
ms.openlocfilehash: 0528d660f590e106f61729f10f8f68da3fe58cb7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="secure-access-to-your-logic-apps"></a><span data-ttu-id="e49fd-103">安全存取您的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="e49fd-103">Secure access to your logic apps</span></span>

<span data-ttu-id="e49fd-104">有許多工具可用來協助您保護您的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e49fd-104">There are many tools available to help you secure your logic app.</span></span>

* <span data-ttu-id="e49fd-105">保護觸發邏輯應用程式的存取 (HTTP 要求觸發程序)</span><span class="sxs-lookup"><span data-stu-id="e49fd-105">Securing access to trigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="e49fd-106">保護管理、編輯或讀取邏輯應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-106">Securing access to manage, edit, or read a logic app</span></span>
* <span data-ttu-id="e49fd-107">保護輸入內容與執行輸出的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-107">Securing access to contents of inputs and outputs for a run</span></span>
* <span data-ttu-id="e49fd-108">保護工作流程中動作內的參數或輸入</span><span class="sxs-lookup"><span data-stu-id="e49fd-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="e49fd-109">保護接受工作流程要求之服務的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-109">Securing access to services that receive requests from a workflow</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="e49fd-110">保護觸發程序的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-110">Secure access to trigger</span></span>

<span data-ttu-id="e49fd-111">當您使用透過 HTTP 要求 ([要求](../connectors/connectors-native-reqres.md)或 [Webhook](../connectors/connectors-native-webhook.md)) 引發的邏輯應用程式時，您可以限制存取，讓只有經過授權的用戶端可以引發該邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e49fd-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="e49fd-112">所有傳入邏輯應用程式的要求都會透過 SSL 加密並保護。</span><span class="sxs-lookup"><span data-stu-id="e49fd-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="e49fd-113">共用存取簽章</span><span class="sxs-lookup"><span data-stu-id="e49fd-113">Shared Access Signature</span></span>

<span data-ttu-id="e49fd-114">邏輯應用程式的每個要求端點都會在 URL 中包含[共用存取簽章](../storage/common/storage-dotnet-shared-access-signature-part-1.md) (SAS)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="e49fd-115">每個 URL 都包含 `sp`、`sv` 和 `sig` 查詢參數。</span><span class="sxs-lookup"><span data-stu-id="e49fd-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="e49fd-116">`sp` 會指定權限，並對應至允許的 HTTP 方法，`sv` 是用來產生的版本，而 `sig` 是用來驗證對觸發程序的存取。</span><span class="sxs-lookup"><span data-stu-id="e49fd-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="e49fd-117">簽章是使用 SHA256 演算法搭配秘密金鑰所產生，位於所有的 URL 路徑和屬性上。</span><span class="sxs-lookup"><span data-stu-id="e49fd-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="e49fd-118">秘密金鑰永遠不會公開及發佈，並且會維持加密狀態，儲存於邏輯應用程式中。</span><span class="sxs-lookup"><span data-stu-id="e49fd-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="e49fd-119">您的邏輯應用程式只會針對包含使用秘密金鑰建立之有效簽章的觸發程序進行授權。</span><span class="sxs-lookup"><span data-stu-id="e49fd-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="e49fd-120">重新產生存取金鑰</span><span class="sxs-lookup"><span data-stu-id="e49fd-120">Regenerate access keys</span></span>

<span data-ttu-id="e49fd-121">您可以隨時透過 REST API 或 Azure 入口網站重新產生新的安全金鑰。</span><span class="sxs-lookup"><span data-stu-id="e49fd-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="e49fd-122">之前使用舊金鑰產生的所有目前 URL 都將失效，並且不再有引發邏輯應用程式的授權。</span><span class="sxs-lookup"><span data-stu-id="e49fd-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="e49fd-123">在 Azure 入口網站中，開啟您要重新產生金鑰的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="e49fd-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="e49fd-124">按一下 [設定] 之下的 [存取金鑰] 功能表項目</span><span class="sxs-lookup"><span data-stu-id="e49fd-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="e49fd-125">選擇要重新產生的金鑰並完成程序</span><span class="sxs-lookup"><span data-stu-id="e49fd-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="e49fd-126">重新產生之後，您所擷取的 URL 會使用新的存取金鑰進行簽署。</span><span class="sxs-lookup"><span data-stu-id="e49fd-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="e49fd-127">使用具有到期日期的回呼 URL</span><span class="sxs-lookup"><span data-stu-id="e49fd-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="e49fd-128">如果您與其他人共用 URL，您可以視需要產生具有特定金鑰和到期日期的 URL。</span><span class="sxs-lookup"><span data-stu-id="e49fd-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="e49fd-129">您之後就能順暢地輪替金鑰，或是確保引發應用程式的存取權限制於特定的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e49fd-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="e49fd-130">您可以透過[邏輯應用程式 REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) 指定 URL 的到期日期：</span><span class="sxs-lookup"><span data-stu-id="e49fd-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="e49fd-131">在主體中，包含屬性 `NotAfter` 做為 JSON 日期字串，這會傳回僅在 `NotAfter` 日期與時間之前有效的回呼 URL。</span><span class="sxs-lookup"><span data-stu-id="e49fd-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="e49fd-132">建立具有主要或次要秘密金鑰的 URL</span><span class="sxs-lookup"><span data-stu-id="e49fd-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="e49fd-133">當您針對要求式觸發程序產生或是列出回呼 URL 時，您也可以指定要用來簽署 URL 的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e49fd-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="e49fd-134">您可以透過[邏輯應用程式 REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) 產生以特定金鑰簽署的 URL，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e49fd-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="e49fd-135">在主體中，將屬性 `KeyType` 包含為 `Primary` 或 `Secondary`。</span><span class="sxs-lookup"><span data-stu-id="e49fd-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="e49fd-136">這會傳回以指定之安全金鑰簽署的 URL。</span><span class="sxs-lookup"><span data-stu-id="e49fd-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="e49fd-137">限制傳入的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="e49fd-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="e49fd-138">除了共用存取簽章，您應該會想要限制只從特定用戶端呼叫邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e49fd-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="e49fd-139">例如，如果您透過 Azure API 管理來管理端點，您可以限制邏輯應用程式僅接受來自 API 管理實體之 IP 位址的要求。</span><span class="sxs-lookup"><span data-stu-id="e49fd-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="e49fd-140">此設定可在邏輯應用程式設定中進行設定：</span><span class="sxs-lookup"><span data-stu-id="e49fd-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="e49fd-141">在 Azure 入口網站中，開啟您要新增 IP 位址限制的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="e49fd-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="e49fd-142">按一下 [設定] 之下的 [存取控制設定] 功能表項目</span><span class="sxs-lookup"><span data-stu-id="e49fd-142">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="e49fd-143">指定觸發程序可接受的 IP 位址範圍清單</span><span class="sxs-lookup"><span data-stu-id="e49fd-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="e49fd-144">有效的 IP 位址範圍格式為 `192.168.1.1/255`。</span><span class="sxs-lookup"><span data-stu-id="e49fd-144">A valid IP range takes the format `192.168.1.1/255`.</span></span> <span data-ttu-id="e49fd-145">如果您只想讓邏輯應用程式做為巢狀邏輯應用程式進行引發，請選取 [僅其他邏輯應用程式] 選項。</span><span class="sxs-lookup"><span data-stu-id="e49fd-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="e49fd-146">這個選項會將空陣列寫入資源，表示只能成功引發來自服務本身 (父邏輯應用程式) 的呼叫。</span><span class="sxs-lookup"><span data-stu-id="e49fd-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="e49fd-147">您仍然可以透過 REST API / Management `/triggers/{triggerName}/run` 來執行含有要求觸發程序的邏輯應用程式，不論 IP 位址為何。</span><span class="sxs-lookup"><span data-stu-id="e49fd-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="e49fd-148">在此情況下，會要求針對 Azure REST API 進行驗證，而所有事件都會出現在 Azure 稽核記錄中。</span><span class="sxs-lookup"><span data-stu-id="e49fd-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="e49fd-149">請適當地設定存取控制原則。</span><span class="sxs-lookup"><span data-stu-id="e49fd-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="e49fd-150">在資源定義上設定 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="e49fd-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="e49fd-151">如果您使用[部署範本](logic-apps-create-deploy-template.md)來自動化您的部署，您可以在資源範本上設定 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="e49fd-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

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

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="e49fd-152">新增 Azure Active Directory、OAuth 或其他安全性</span><span class="sxs-lookup"><span data-stu-id="e49fd-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="e49fd-153">為了在邏輯應用程式最上層新增更多授權通訊協定，[Azure API 管理](https://azure.microsoft.com/services/api-management/)針對任何能夠將邏輯應用程式公開為 API 的端點，提供豐富的監控、安全性、原則和文件。</span><span class="sxs-lookup"><span data-stu-id="e49fd-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="e49fd-154">Azure API 管理可針對邏輯應用程式將公用或私人端點公開，並且可以使用 Azure Active Directory、憑證、OAuth 或其他的安全性標準。</span><span class="sxs-lookup"><span data-stu-id="e49fd-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="e49fd-155">收到要求時，Azure API 管理會將要求轉送至邏輯應用程式 (並在過程中執行任何必要的轉換或限制)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="e49fd-156">您可以在邏輯應用程式上使用傳入 IP 範圍設定，讓邏輯應用程式只能透過 API 管理觸發。</span><span class="sxs-lookup"><span data-stu-id="e49fd-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="e49fd-157">保護管理或編輯邏輯應用程式的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="e49fd-158">您可以限制邏輯應用程式的管理作業存取，以便只有特定的使用者或群組能夠在資源上執行操作。</span><span class="sxs-lookup"><span data-stu-id="e49fd-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="e49fd-159">邏輯應用程式使用 Azure [角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md) 功能，並且能夠使用相同的工具進行自訂。</span><span class="sxs-lookup"><span data-stu-id="e49fd-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="e49fd-160">您也可以將一些內建的角色指派給訂用帳戶的成員：</span><span class="sxs-lookup"><span data-stu-id="e49fd-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="e49fd-161">**邏輯應用程式參與者**：提供邏輯應用程式檢視、編輯和更新的存取權限。</span><span class="sxs-lookup"><span data-stu-id="e49fd-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="e49fd-162">無法移除資源或執行管理作業。</span><span class="sxs-lookup"><span data-stu-id="e49fd-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="e49fd-163">**邏輯應用程式操作員**：可以檢視邏輯應用程式和執行歷程記錄，以及啟用/停用。</span><span class="sxs-lookup"><span data-stu-id="e49fd-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="e49fd-164">無法編輯或更新定義。</span><span class="sxs-lookup"><span data-stu-id="e49fd-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="e49fd-165">您也可以使用 [Azure 資源鎖定](../azure-resource-manager/resource-group-lock-resources.md)，來防止變更或刪除邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="e49fd-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="e49fd-166">這個功能對於防止生產資源遭到修改或刪除非常有用。</span><span class="sxs-lookup"><span data-stu-id="e49fd-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="e49fd-167">保護執行歷程記錄內容的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="e49fd-168">您可以將輸入的內容，或是先前所執行的輸出，限制為只有特定 IP 位址範圍可以存取。</span><span class="sxs-lookup"><span data-stu-id="e49fd-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="e49fd-169">工作流程執行中的所有資料在傳輸及靜止時都會加密。</span><span class="sxs-lookup"><span data-stu-id="e49fd-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="e49fd-170">對執行歷程記錄進行呼叫時，服務會驗證要求、提供要求的連結，並回應輸入並輸出。</span><span class="sxs-lookup"><span data-stu-id="e49fd-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="e49fd-171">此連結會受到保護，以確保只有來自指定 IP 位址範圍的檢視內容要求才會傳回內容。</span><span class="sxs-lookup"><span data-stu-id="e49fd-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="e49fd-172">您可以使用此功能來進行其他存取控制。</span><span class="sxs-lookup"><span data-stu-id="e49fd-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="e49fd-173">您甚至可以指定如 `0.0.0.0` 的 IP 位址，這樣就沒有人可以存取輸入/輸出。</span><span class="sxs-lookup"><span data-stu-id="e49fd-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="e49fd-174">只有具備管理員權限的人才能移除此限制，提供工作流程內容「即時」存取的可能性。</span><span class="sxs-lookup"><span data-stu-id="e49fd-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="e49fd-175">這個設定可在 Azure 入口網站的資源設定中進行設定：</span><span class="sxs-lookup"><span data-stu-id="e49fd-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="e49fd-176">在 Azure 入口網站中，開啟您要新增 IP 位址限制的邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="e49fd-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="e49fd-177">按一下 [設定] 之下的 [存取控制設定] 功能表項目</span><span class="sxs-lookup"><span data-stu-id="e49fd-177">Click the **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="e49fd-178">針對內容的存取指定 IP 位址範圍清單</span><span class="sxs-lookup"><span data-stu-id="e49fd-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="e49fd-179">在資源定義上設定 IP 範圍</span><span class="sxs-lookup"><span data-stu-id="e49fd-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="e49fd-180">如果您使用[部署範本](logic-apps-create-deploy-template.md)來自動化您的部署，您可以在資源範本上設定 IP 範圍。</span><span class="sxs-lookup"><span data-stu-id="e49fd-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

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

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="e49fd-181">保護工作流程中的參數和輸入</span><span class="sxs-lookup"><span data-stu-id="e49fd-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="e49fd-182">您可能想要將工作流程定義的某些層面參數化，以便跨環境進行部署。</span><span class="sxs-lookup"><span data-stu-id="e49fd-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="e49fd-183">此外，部分參數可能是您不想在編輯工作流程時顯示的安全參數，例如 HTTP 動作的 [Azure Active Directory 驗證](../connectors/connectors-native-http.md#authentication)的用戶端識別碼和用戶端密碼。</span><span class="sxs-lookup"><span data-stu-id="e49fd-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="e49fd-184">使用參數和安全參數</span><span class="sxs-lookup"><span data-stu-id="e49fd-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="e49fd-185">為了在執行階段存取資源參數的值，[工作流程定義語言 (英文)](http://aka.ms/logicappsdocs) 提供 `@parameters()` 作業。</span><span class="sxs-lookup"><span data-stu-id="e49fd-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="e49fd-186">此外，您可以[指定資源部署範本中的參數](../azure-resource-manager/resource-group-authoring-templates.md#parameters)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="e49fd-187">但是，如果您將參數類型指定為 `securestring`，將無法透過其餘的資源定義傳回此參數，而且在部署之後，將無法藉由檢視資源存取此資源。</span><span class="sxs-lookup"><span data-stu-id="e49fd-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="e49fd-188">如果您在要求的標頭或主體中使用參數，可藉由存取執行歷程記錄及連出 HTTP 要求來檢視該參數。</span><span class="sxs-lookup"><span data-stu-id="e49fd-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="e49fd-189">請務必適當地設定您的內容存取原則。</span><span class="sxs-lookup"><span data-stu-id="e49fd-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="e49fd-190">授權標頭絕對不會透過輸入或輸出來顯示。</span><span class="sxs-lookup"><span data-stu-id="e49fd-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="e49fd-191">因此，如果該處使用了密碼，就無法擷取該密碼。</span><span class="sxs-lookup"><span data-stu-id="e49fd-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="e49fd-192">含有密碼的資源部署範本</span><span class="sxs-lookup"><span data-stu-id="e49fd-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="e49fd-193">下列範例示範在執行階段中參考 `secret` 安全參數的部署。</span><span class="sxs-lookup"><span data-stu-id="e49fd-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="e49fd-194">在個別的參數檔中，您可以指定 `secret` 的環境值，或是利用 [Azure Resource Manager Key Vault](../azure-resource-manager/resource-manager-keyvault-parameter.md)，在部署階段擷取密碼。</span><span class="sxs-lookup"><span data-stu-id="e49fd-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

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
                "body": "This is the request"
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

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="e49fd-195">保護接受工作流程要求之服務的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="e49fd-196">有許多方法可以協助保護邏輯應用程式需要存取的所有端點。</span><span class="sxs-lookup"><span data-stu-id="e49fd-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="e49fd-197">在外送要求上使用驗證</span><span class="sxs-lookup"><span data-stu-id="e49fd-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="e49fd-198">當使用 HTTP、HTTP + Swagger (Open API)，或 Webhook 動作時，您可以將驗證新增到所傳送的要求。</span><span class="sxs-lookup"><span data-stu-id="e49fd-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="e49fd-199">您可以包括基本驗證、憑證驗證或 Azure Active Directory 驗證。</span><span class="sxs-lookup"><span data-stu-id="e49fd-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="e49fd-200">如需如何設定此驗證的詳細資料，請參閱[此文章](../connectors/connectors-native-http.md#authentication)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="e49fd-201">限制對邏輯應用程式 IP 位址的存取</span><span class="sxs-lookup"><span data-stu-id="e49fd-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="e49fd-202">邏輯應用程式的所有呼叫都來自每個區域一組特定的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e49fd-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="e49fd-203">您可以加入其他篩選以僅允許接受來自那些指定 IP 位址的要求。</span><span class="sxs-lookup"><span data-stu-id="e49fd-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="e49fd-204">如需這些 IP 位址清單，請參閱[邏輯應用程式的限制和設定](logic-apps-limits-and-config.md#configuration)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="e49fd-205">內部部署連線能力</span><span class="sxs-lookup"><span data-stu-id="e49fd-205">On-premises connectivity</span></span>

<span data-ttu-id="e49fd-206">邏輯應用程式提供與數個服務的整合，以提供安全可靠的內部部署通訊。</span><span class="sxs-lookup"><span data-stu-id="e49fd-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="e49fd-207">內部部署資料閘道</span><span class="sxs-lookup"><span data-stu-id="e49fd-207">On-premises data gateway</span></span>

<span data-ttu-id="e49fd-208">邏輯應用程式的許多受管理連接器提供對內部部署系統 (包括檔案系統、SQL、SharePoint、DB2 等等) 的安全連線能力。</span><span class="sxs-lookup"><span data-stu-id="e49fd-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="e49fd-209">閘道會在加密通道上經過 Azure 服務匯流排轉送來自內部部署來源的資料。</span><span class="sxs-lookup"><span data-stu-id="e49fd-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="e49fd-210">源自閘道代理程式的所有流量都是安全輸出流量。</span><span class="sxs-lookup"><span data-stu-id="e49fd-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="e49fd-211">深入了解[資料閘道的運作方式](logic-apps-gateway-install.md#gateway-cloud-service)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="e49fd-212">Azure API 管理</span><span class="sxs-lookup"><span data-stu-id="e49fd-212">Azure API Management</span></span>

<span data-ttu-id="e49fd-213">[Azure API 管理](https://azure.microsoft.com/services/api-management/)具有內部部署連線選項，包括站對站 VPN 和 ExpressRoute 整合，以對內部部署系統提供安全的 Proxy 和通訊。</span><span class="sxs-lookup"><span data-stu-id="e49fd-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="e49fd-214">在邏輯應用程式設計工具中，您可以在工作流程中快速地選取從 Azure API 管理公開的 API，提供對內部部署系統的快速存取。</span><span class="sxs-lookup"><span data-stu-id="e49fd-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="e49fd-215">Azure App Service 的混合式連線</span><span class="sxs-lookup"><span data-stu-id="e49fd-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="e49fd-216">您可以使用 Azure API 和 Web 應用程式的內部部署混合式連線功能，以對內部部署進行通訊。</span><span class="sxs-lookup"><span data-stu-id="e49fd-216">You can use the on-premises hybrid connection feature for Azure API and Web apps to communicate on-premises.</span></span>  <span data-ttu-id="e49fd-217">如需混合式連線的詳細資料和設定方式，請參閱[此文章](../app-service-web/web-sites-hybrid-connection-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="e49fd-217">Details on hybrid connections and how to configure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e49fd-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e49fd-218">Next steps</span></span>
[<span data-ttu-id="e49fd-219">建立部署範本</span><span class="sxs-lookup"><span data-stu-id="e49fd-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="e49fd-220">例外狀況處理</span><span class="sxs-lookup"><span data-stu-id="e49fd-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="e49fd-221">監視邏輯應用程式</span><span class="sxs-lookup"><span data-stu-id="e49fd-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="e49fd-222">診斷邏輯應用程式失敗和問題</span><span class="sxs-lookup"><span data-stu-id="e49fd-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
