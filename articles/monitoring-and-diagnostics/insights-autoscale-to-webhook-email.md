---
title: "aaaUse 自動調整規模動作 toosend 電子郵件和 webhook 警示通知。 | Microsoft Docs"
description: "請參閱 toouse 自動調整規模動作 toocall web Url 或 Azure 監視器中傳送電子郵件通知的方式。 "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="5d6b6-104">使用 Azure 監視器 」 中的自動調整規模動作 toosend 電子郵件和 webhook 警示通知</span><span class="sxs-lookup"><span data-stu-id="5d6b6-104">Use autoscale actions toosend email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="5d6b6-105">本文將告訴您如何設定觸發程序，讓您可以根據 Azure 中的自動調整動作呼叫特定的 Web URl 或傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="5d6b6-106">Webhook</span><span class="sxs-lookup"><span data-stu-id="5d6b6-106">Webhooks</span></span>
<span data-ttu-id="5d6b6-107">Webhook 允許 tooroute hello Azure 的警示通知 tooother 系統後置處理或自訂通知。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-107">Webhooks allow you tooroute hello Azure alert notifications tooother systems for post-processing or custom notifications.</span></span> <span data-ttu-id="5d6b6-108">例如，可處理連入 web 要求 toosend SMS，記錄錯誤，路由 hello 警示 tooservices 通知小組使用聊天室訊息服務，等 hello webhook URI 必須是有效的 HTTP 或 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-108">For example, routing hello alert tooservices that can handle an incoming web request toosend SMS, log bugs, notify a team using chat or messaging services, etc. hello webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="5d6b6-109">電子郵件</span><span class="sxs-lookup"><span data-stu-id="5d6b6-109">Email</span></span>
<span data-ttu-id="5d6b6-110">可以 tooany 有效的電子郵件地址傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-110">Email can be sent tooany valid email address.</span></span> <span data-ttu-id="5d6b6-111">系統也會通知系統管理員和共同管理員的 hello hello 規則執行所在的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-111">Administrators and co-administrators of hello subscription where hello rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="5d6b6-112">雲端服務和 Web Apps</span><span class="sxs-lookup"><span data-stu-id="5d6b6-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="5d6b6-113">您可以在選擇 hello Azure 入口網站從雲端服務和伺服器陣列 （Web 應用程式）。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-113">You can opt-in from hello Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="5d6b6-114">選擇 hello**縮放**度量。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-114">Choose hello **scale by** metric.</span></span>

![調整依據](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="5d6b6-116">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="5d6b6-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="5d6b6-117">對於使用 Resource Manager 建立的較新虛擬機器 (虛擬機器擴展集)，您可以使用 REST API、Resource Manager 範本、PowerShell 和 CLI 設定此項目。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="5d6b6-118">目前尚無入口網站介面。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="5d6b6-119">使用 REST API hello 或資源管理員範本時，包含下列選項的 hello hello 通知項目。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-119">When using hello REST API or Resource Manager template, include hello notifications element with hello following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="5d6b6-120">欄位</span><span class="sxs-lookup"><span data-stu-id="5d6b6-120">Field</span></span> | <span data-ttu-id="5d6b6-121">是否為強制？</span><span class="sxs-lookup"><span data-stu-id="5d6b6-121">Mandatory?</span></span> | <span data-ttu-id="5d6b6-122">說明</span><span class="sxs-lookup"><span data-stu-id="5d6b6-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d6b6-123">operation</span><span class="sxs-lookup"><span data-stu-id="5d6b6-123">operation</span></span> |<span data-ttu-id="5d6b6-124">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-124">yes</span></span> |<span data-ttu-id="5d6b6-125">值必須是 [調整]</span><span class="sxs-lookup"><span data-stu-id="5d6b6-125">value must be "Scale"</span></span> |
| <span data-ttu-id="5d6b6-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="5d6b6-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="5d6b6-127">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-127">yes</span></span> |<span data-ttu-id="5d6b6-128">值必須是 "true" 或 "false"</span><span class="sxs-lookup"><span data-stu-id="5d6b6-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="5d6b6-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="5d6b6-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="5d6b6-130">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-130">yes</span></span> |<span data-ttu-id="5d6b6-131">值必須是 "true" 或 "false"</span><span class="sxs-lookup"><span data-stu-id="5d6b6-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="5d6b6-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="5d6b6-132">customEmails</span></span> |<span data-ttu-id="5d6b6-133">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-133">yes</span></span> |<span data-ttu-id="5d6b6-134">值可以是 null 或電子郵件的字串陣列</span><span class="sxs-lookup"><span data-stu-id="5d6b6-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="5d6b6-135">Webhook</span><span class="sxs-lookup"><span data-stu-id="5d6b6-135">webhooks</span></span> |<span data-ttu-id="5d6b6-136">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-136">yes</span></span> |<span data-ttu-id="5d6b6-137">值可以是 null 或有效的 Uri</span><span class="sxs-lookup"><span data-stu-id="5d6b6-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="5d6b6-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="5d6b6-138">serviceUri</span></span> |<span data-ttu-id="5d6b6-139">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-139">yes</span></span> |<span data-ttu-id="5d6b6-140">有效的 https Uri</span><span class="sxs-lookup"><span data-stu-id="5d6b6-140">a valid https Uri</span></span> |
| <span data-ttu-id="5d6b6-141">properties</span><span class="sxs-lookup"><span data-stu-id="5d6b6-141">properties</span></span> |<span data-ttu-id="5d6b6-142">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-142">yes</span></span> |<span data-ttu-id="5d6b6-143">值必須是空的 {}，或可以包含索引鍵-值組</span><span class="sxs-lookup"><span data-stu-id="5d6b6-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="5d6b6-144">Webhook 中的驗證</span><span class="sxs-lookup"><span data-stu-id="5d6b6-144">Authentication in webhooks</span></span>
<span data-ttu-id="5d6b6-145">hello webhook 可以驗證使用權杖型驗證，您將 hello webhook URI 儲存為查詢參數的權杖識別碼。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-145">hello webhook can authenticate using token-based authentication, where you save hello webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="5d6b6-146">例如，https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="5d6b6-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="5d6b6-147">自動調整通知 Webhook 承載結構描述</span><span class="sxs-lookup"><span data-stu-id="5d6b6-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="5d6b6-148">當產生 hello 自動調整規模通知時，hello 下列中繼資料包含在 hello webhook 裝載：</span><span class="sxs-lookup"><span data-stu-id="5d6b6-148">When hello autoscale notification is generated, hello following metadata is included in hello webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="5d6b6-149">欄位</span><span class="sxs-lookup"><span data-stu-id="5d6b6-149">Field</span></span> | <span data-ttu-id="5d6b6-150">是否為強制？</span><span class="sxs-lookup"><span data-stu-id="5d6b6-150">Mandatory?</span></span> | <span data-ttu-id="5d6b6-151">說明</span><span class="sxs-lookup"><span data-stu-id="5d6b6-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5d6b6-152">status</span><span class="sxs-lookup"><span data-stu-id="5d6b6-152">status</span></span> |<span data-ttu-id="5d6b6-153">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-153">yes</span></span> |<span data-ttu-id="5d6b6-154">表示所產生的自動調整規模動作 hello 狀態</span><span class="sxs-lookup"><span data-stu-id="5d6b6-154">hello status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="5d6b6-155">operation</span><span class="sxs-lookup"><span data-stu-id="5d6b6-155">operation</span></span> |<span data-ttu-id="5d6b6-156">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-156">yes</span></span> |<span data-ttu-id="5d6b6-157">若執行個體增加，它會「相應放大」，若執行個體減少，它會「相應縮小」。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="5d6b6-158">context</span><span class="sxs-lookup"><span data-stu-id="5d6b6-158">context</span></span> |<span data-ttu-id="5d6b6-159">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-159">yes</span></span> |<span data-ttu-id="5d6b6-160">hello 自動調整規模動作內容</span><span class="sxs-lookup"><span data-stu-id="5d6b6-160">hello autoscale action context</span></span> |
| <span data-ttu-id="5d6b6-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="5d6b6-161">timestamp</span></span> |<span data-ttu-id="5d6b6-162">yes</span><span class="sxs-lookup"><span data-stu-id="5d6b6-162">yes</span></span> |<span data-ttu-id="5d6b6-163">觸發 hello 自動調整規模動作時的時間戳記</span><span class="sxs-lookup"><span data-stu-id="5d6b6-163">Time stamp when hello autoscale action was triggered</span></span> |
| <span data-ttu-id="5d6b6-164">id</span><span class="sxs-lookup"><span data-stu-id="5d6b6-164">id</span></span> |<span data-ttu-id="5d6b6-165">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-165">Yes</span></span> |<span data-ttu-id="5d6b6-166">資源管理員識別碼 hello 自動調整規模設定</span><span class="sxs-lookup"><span data-stu-id="5d6b6-166">Resource Manager ID of hello autoscale setting</span></span> |
| <span data-ttu-id="5d6b6-167">名稱</span><span class="sxs-lookup"><span data-stu-id="5d6b6-167">name</span></span> |<span data-ttu-id="5d6b6-168">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-168">Yes</span></span> |<span data-ttu-id="5d6b6-169">hello hello 自動調整規模設定名稱</span><span class="sxs-lookup"><span data-stu-id="5d6b6-169">hello name of hello autoscale setting</span></span> |
| <span data-ttu-id="5d6b6-170">詳細資料</span><span class="sxs-lookup"><span data-stu-id="5d6b6-170">details</span></span> |<span data-ttu-id="5d6b6-171">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-171">Yes</span></span> |<span data-ttu-id="5d6b6-172">Hello 自動調整規模服務的 hello 動作的說明，並 hello 變更 hello 執行個體計數</span><span class="sxs-lookup"><span data-stu-id="5d6b6-172">Explanation of hello action that hello autoscale service took and hello change in hello instance count</span></span> |
| <span data-ttu-id="5d6b6-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="5d6b6-173">subscriptionId</span></span> |<span data-ttu-id="5d6b6-174">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-174">Yes</span></span> |<span data-ttu-id="5d6b6-175">已縮放的 hello 目標資源的訂用帳戶 ID</span><span class="sxs-lookup"><span data-stu-id="5d6b6-175">Subscription ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="5d6b6-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="5d6b6-176">resourceGroupName</span></span> |<span data-ttu-id="5d6b6-177">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-177">Yes</span></span> |<span data-ttu-id="5d6b6-178">已縮放的 hello 目標資源的資源群組名稱</span><span class="sxs-lookup"><span data-stu-id="5d6b6-178">Resource Group name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="5d6b6-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="5d6b6-179">resourceName</span></span> |<span data-ttu-id="5d6b6-180">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-180">Yes</span></span> |<span data-ttu-id="5d6b6-181">已縮放的 hello 目標資源的名稱</span><span class="sxs-lookup"><span data-stu-id="5d6b6-181">Name of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="5d6b6-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="5d6b6-182">resourceType</span></span> |<span data-ttu-id="5d6b6-183">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-183">Yes</span></span> |<span data-ttu-id="5d6b6-184">hello 三個支援的值:"microsoft.classiccompute/domainnames/slots/roles"-雲端服務角色、 「 microsoft.compute/virtualmachinescalesets"-虛擬機器擴展集和 「 Microsoft.Web/serverfarms"-Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="5d6b6-184">hello three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="5d6b6-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="5d6b6-185">resourceId</span></span> |<span data-ttu-id="5d6b6-186">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-186">Yes</span></span> |<span data-ttu-id="5d6b6-187">已縮放的 hello 目標資源的資源管理員識別碼</span><span class="sxs-lookup"><span data-stu-id="5d6b6-187">Resource Manager ID of hello target resource that is being scaled</span></span> |
| <span data-ttu-id="5d6b6-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="5d6b6-188">portalLink</span></span> |<span data-ttu-id="5d6b6-189">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-189">Yes</span></span> |<span data-ttu-id="5d6b6-190">Azure 入口網站的連結 toohello 摘要 頁面上的 hello 目標資源</span><span class="sxs-lookup"><span data-stu-id="5d6b6-190">Azure portal link toohello summary page of hello target resource</span></span> |
| <span data-ttu-id="5d6b6-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="5d6b6-191">oldCapacity</span></span> |<span data-ttu-id="5d6b6-192">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-192">Yes</span></span> |<span data-ttu-id="5d6b6-193">hello 目前 （舊） 執行個體計數時自動調整規模所需的調整規模動作</span><span class="sxs-lookup"><span data-stu-id="5d6b6-193">hello current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="5d6b6-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="5d6b6-194">newCapacity</span></span> |<span data-ttu-id="5d6b6-195">是</span><span class="sxs-lookup"><span data-stu-id="5d6b6-195">Yes</span></span> |<span data-ttu-id="5d6b6-196">hello 自動調整規模調整 hello 資源太新執行個體計數</span><span class="sxs-lookup"><span data-stu-id="5d6b6-196">hello new instance count that Autoscale scaled hello resource too</span></span>|
| <span data-ttu-id="5d6b6-197">屬性</span><span class="sxs-lookup"><span data-stu-id="5d6b6-197">Properties</span></span> |<span data-ttu-id="5d6b6-198">否</span><span class="sxs-lookup"><span data-stu-id="5d6b6-198">No</span></span> |<span data-ttu-id="5d6b6-199">選用。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-199">Optional.</span></span> <span data-ttu-id="5d6b6-200"><索引鍵, 值> 組 (例如，字典 <字串, 字串>)。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="5d6b6-201">hello 屬性欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-201">hello properties field is optional.</span></span> <span data-ttu-id="5d6b6-202">您可以在自訂使用者介面或邏輯基礎的應用程式工作流程中，輸入索引鍵和值，可使用 hello 裝載傳遞。</span><span class="sxs-lookup"><span data-stu-id="5d6b6-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using hello payload.</span></span> <span data-ttu-id="5d6b6-203">Toopass 自訂屬性 back toohello 外寄的 webhook 呼叫的替代方式是 toouse hello webhook URI 本身 （作為查詢參數）</span><span class="sxs-lookup"><span data-stu-id="5d6b6-203">An alternate way toopass custom properties back toohello outgoing webhook call is toouse hello webhook URI itself (as query parameters)</span></span> |
