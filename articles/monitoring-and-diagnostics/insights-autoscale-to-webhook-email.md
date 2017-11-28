---
title: "使用自動調整動作傳送電子郵件和 Webhook 警示通知 | Microsoft Docs"
description: "了解如何在 Azure 監視器中使用自動調整動作呼叫 Web URL 或傳送電子郵件通知。 "
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
ms.openlocfilehash: 16caf14028494800e9259f0296c292b606d0210a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="f142d-104">使用自動調整動作在 Azure 監視器中傳送電子郵件和 Webhook 警示通知</span><span class="sxs-lookup"><span data-stu-id="f142d-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="f142d-105">本文將告訴您如何設定觸發程序，讓您可以根據 Azure 中的自動調整動作呼叫特定的 Web URl 或傳送電子郵件。</span><span class="sxs-lookup"><span data-stu-id="f142d-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="f142d-106">Webhook</span><span class="sxs-lookup"><span data-stu-id="f142d-106">Webhooks</span></span>
<span data-ttu-id="f142d-107">Webhook 可讓您將 Azure 警示通知路由到其他系統進行後處理或自訂通知。</span><span class="sxs-lookup"><span data-stu-id="f142d-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="f142d-108">例如，將警示路由到可處理傳入 Web 要求的服務，以傳送 SMS、記錄錯誤、使用聊天或傳訊服務通知團隊等等。Webhook URI 必須是有效的 HTTP 或 HTTPS 端點。</span><span class="sxs-lookup"><span data-stu-id="f142d-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="f142d-109">電子郵件</span><span class="sxs-lookup"><span data-stu-id="f142d-109">Email</span></span>
<span data-ttu-id="f142d-110">電子郵件可以傳送至任何有效的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="f142d-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="f142d-111">也會通知執行該規則的訂用帳戶的系統管理員和共同管理員。</span><span class="sxs-lookup"><span data-stu-id="f142d-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="f142d-112">雲端服務和 Web Apps</span><span class="sxs-lookup"><span data-stu-id="f142d-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="f142d-113">您可以在 Azure 的雲端服務和伺服器陣列 (Web Apps) 入口網站中選擇加入。</span><span class="sxs-lookup"><span data-stu-id="f142d-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="f142d-114">選擇做為 [調整依據]  的度量。</span><span class="sxs-lookup"><span data-stu-id="f142d-114">Choose the **scale by** metric.</span></span>

![調整依據](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="f142d-116">虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="f142d-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="f142d-117">對於使用 Resource Manager 建立的較新虛擬機器 (虛擬機器擴展集)，您可以使用 REST API、Resource Manager 範本、PowerShell 和 CLI 設定此項目。</span><span class="sxs-lookup"><span data-stu-id="f142d-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="f142d-118">目前尚無入口網站介面。</span><span class="sxs-lookup"><span data-stu-id="f142d-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="f142d-119">當您使用 REST API 或 Resource Manager 範本時，請在下列選項中包含通知項目。</span><span class="sxs-lookup"><span data-stu-id="f142d-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="f142d-120">欄位</span><span class="sxs-lookup"><span data-stu-id="f142d-120">Field</span></span> | <span data-ttu-id="f142d-121">是否為強制？</span><span class="sxs-lookup"><span data-stu-id="f142d-121">Mandatory?</span></span> | <span data-ttu-id="f142d-122">說明</span><span class="sxs-lookup"><span data-stu-id="f142d-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f142d-123">operation</span><span class="sxs-lookup"><span data-stu-id="f142d-123">operation</span></span> |<span data-ttu-id="f142d-124">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-124">yes</span></span> |<span data-ttu-id="f142d-125">值必須是 [調整]</span><span class="sxs-lookup"><span data-stu-id="f142d-125">value must be "Scale"</span></span> |
| <span data-ttu-id="f142d-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="f142d-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="f142d-127">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-127">yes</span></span> |<span data-ttu-id="f142d-128">值必須是 "true" 或 "false"</span><span class="sxs-lookup"><span data-stu-id="f142d-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="f142d-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="f142d-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="f142d-130">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-130">yes</span></span> |<span data-ttu-id="f142d-131">值必須是 "true" 或 "false"</span><span class="sxs-lookup"><span data-stu-id="f142d-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="f142d-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="f142d-132">customEmails</span></span> |<span data-ttu-id="f142d-133">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-133">yes</span></span> |<span data-ttu-id="f142d-134">值可以是 null 或電子郵件的字串陣列</span><span class="sxs-lookup"><span data-stu-id="f142d-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="f142d-135">Webhook</span><span class="sxs-lookup"><span data-stu-id="f142d-135">webhooks</span></span> |<span data-ttu-id="f142d-136">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-136">yes</span></span> |<span data-ttu-id="f142d-137">值可以是 null 或有效的 Uri</span><span class="sxs-lookup"><span data-stu-id="f142d-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="f142d-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="f142d-138">serviceUri</span></span> |<span data-ttu-id="f142d-139">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-139">yes</span></span> |<span data-ttu-id="f142d-140">有效的 https Uri</span><span class="sxs-lookup"><span data-stu-id="f142d-140">a valid https Uri</span></span> |
| <span data-ttu-id="f142d-141">properties</span><span class="sxs-lookup"><span data-stu-id="f142d-141">properties</span></span> |<span data-ttu-id="f142d-142">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-142">yes</span></span> |<span data-ttu-id="f142d-143">值必須是空的 {}，或可以包含索引鍵-值組</span><span class="sxs-lookup"><span data-stu-id="f142d-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="f142d-144">Webhook 中的驗證</span><span class="sxs-lookup"><span data-stu-id="f142d-144">Authentication in webhooks</span></span>
<span data-ttu-id="f142d-145">Webhook 可以使用權杖型驗證來驗證，您會在其中儲存 Webhook URI 並以權杖識別碼做為查詢參數。</span><span class="sxs-lookup"><span data-stu-id="f142d-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="f142d-146">例如，https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="f142d-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="f142d-147">自動調整通知 Webhook 承載結構描述</span><span class="sxs-lookup"><span data-stu-id="f142d-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="f142d-148">產生自動調整通知時，Webhook 承載會包含下列中繼資料︰</span><span class="sxs-lookup"><span data-stu-id="f142d-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
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


| <span data-ttu-id="f142d-149">欄位</span><span class="sxs-lookup"><span data-stu-id="f142d-149">Field</span></span> | <span data-ttu-id="f142d-150">是否為強制？</span><span class="sxs-lookup"><span data-stu-id="f142d-150">Mandatory?</span></span> | <span data-ttu-id="f142d-151">說明</span><span class="sxs-lookup"><span data-stu-id="f142d-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f142d-152">status</span><span class="sxs-lookup"><span data-stu-id="f142d-152">status</span></span> |<span data-ttu-id="f142d-153">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-153">yes</span></span> |<span data-ttu-id="f142d-154">此狀態表示產生了自動調整動作</span><span class="sxs-lookup"><span data-stu-id="f142d-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="f142d-155">operation</span><span class="sxs-lookup"><span data-stu-id="f142d-155">operation</span></span> |<span data-ttu-id="f142d-156">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-156">yes</span></span> |<span data-ttu-id="f142d-157">若執行個體增加，它會「相應放大」，若執行個體減少，它會「相應縮小」。</span><span class="sxs-lookup"><span data-stu-id="f142d-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="f142d-158">context</span><span class="sxs-lookup"><span data-stu-id="f142d-158">context</span></span> |<span data-ttu-id="f142d-159">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-159">yes</span></span> |<span data-ttu-id="f142d-160">自動調整動作內容</span><span class="sxs-lookup"><span data-stu-id="f142d-160">The autoscale action context</span></span> |
| <span data-ttu-id="f142d-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="f142d-161">timestamp</span></span> |<span data-ttu-id="f142d-162">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-162">yes</span></span> |<span data-ttu-id="f142d-163">自動調整動作觸發時的時間戳記</span><span class="sxs-lookup"><span data-stu-id="f142d-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="f142d-164">id</span><span class="sxs-lookup"><span data-stu-id="f142d-164">id</span></span> |<span data-ttu-id="f142d-165">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-165">Yes</span></span> |<span data-ttu-id="f142d-166">自動調整設定的 Resource Manager 識別碼</span><span class="sxs-lookup"><span data-stu-id="f142d-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="f142d-167">名稱</span><span class="sxs-lookup"><span data-stu-id="f142d-167">name</span></span> |<span data-ttu-id="f142d-168">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-168">Yes</span></span> |<span data-ttu-id="f142d-169">自動調整設定的名稱</span><span class="sxs-lookup"><span data-stu-id="f142d-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="f142d-170">詳細資料</span><span class="sxs-lookup"><span data-stu-id="f142d-170">details</span></span> |<span data-ttu-id="f142d-171">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-171">Yes</span></span> |<span data-ttu-id="f142d-172">說明自動調整服務所採取的動作和執行個體計數的變更</span><span class="sxs-lookup"><span data-stu-id="f142d-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="f142d-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="f142d-173">subscriptionId</span></span> |<span data-ttu-id="f142d-174">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-174">Yes</span></span> |<span data-ttu-id="f142d-175">正在調整的目標資源的訂用帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="f142d-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="f142d-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="f142d-176">resourceGroupName</span></span> |<span data-ttu-id="f142d-177">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-177">Yes</span></span> |<span data-ttu-id="f142d-178">正在調整的目標資源的資源群組</span><span class="sxs-lookup"><span data-stu-id="f142d-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="f142d-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="f142d-179">resourceName</span></span> |<span data-ttu-id="f142d-180">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-180">Yes</span></span> |<span data-ttu-id="f142d-181">正在調整的目標資源的名稱</span><span class="sxs-lookup"><span data-stu-id="f142d-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="f142d-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="f142d-182">resourceType</span></span> |<span data-ttu-id="f142d-183">是</span><span class="sxs-lookup"><span data-stu-id="f142d-183">Yes</span></span> |<span data-ttu-id="f142d-184">支援三個值：microsoft.classiccompute/domainnames/slots/roles" (雲端服務角色)、"microsoft.compute/virtualmachinescalesets" (虛擬機器擴展集) 以及 "Microsoft.Web/serverfarms" - (Web 應用程式)</span><span class="sxs-lookup"><span data-stu-id="f142d-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="f142d-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="f142d-185">resourceId</span></span> |<span data-ttu-id="f142d-186">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-186">Yes</span></span> |<span data-ttu-id="f142d-187">正在調整的目標資源的 Resource Manager 識別碼</span><span class="sxs-lookup"><span data-stu-id="f142d-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="f142d-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="f142d-188">portalLink</span></span> |<span data-ttu-id="f142d-189">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-189">Yes</span></span> |<span data-ttu-id="f142d-190">連到目標資源摘要頁面的 Azure 入口網站連結</span><span class="sxs-lookup"><span data-stu-id="f142d-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="f142d-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="f142d-191">oldCapacity</span></span> |<span data-ttu-id="f142d-192">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-192">Yes</span></span> |<span data-ttu-id="f142d-193">自動調整進行調整動作時的當前 (舊) 執行個體計數</span><span class="sxs-lookup"><span data-stu-id="f142d-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="f142d-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="f142d-194">newCapacity</span></span> |<span data-ttu-id="f142d-195">yes</span><span class="sxs-lookup"><span data-stu-id="f142d-195">Yes</span></span> |<span data-ttu-id="f142d-196">自動調整要將資源調整為此數目的新執行個體計數</span><span class="sxs-lookup"><span data-stu-id="f142d-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="f142d-197">properties</span><span class="sxs-lookup"><span data-stu-id="f142d-197">Properties</span></span> |<span data-ttu-id="f142d-198">否</span><span class="sxs-lookup"><span data-stu-id="f142d-198">No</span></span> |<span data-ttu-id="f142d-199">選用。</span><span class="sxs-lookup"><span data-stu-id="f142d-199">Optional.</span></span> <span data-ttu-id="f142d-200"><索引鍵, 值> 組 (例如，字典 <字串, 字串>)。</span><span class="sxs-lookup"><span data-stu-id="f142d-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="f142d-201">properties 欄位是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="f142d-201">The properties field is optional.</span></span> <span data-ttu-id="f142d-202">在自訂 UI 或邏輯應用程式的工作流程中，您可以輸入可使用承載傳遞的索引鍵和值。</span><span class="sxs-lookup"><span data-stu-id="f142d-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="f142d-203">另一個將自訂屬性傳回給連出 Webhook 呼叫的替代做法，是使用 Webhook URI 本身 (做為查詢參數)</span><span class="sxs-lookup"><span data-stu-id="f142d-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
