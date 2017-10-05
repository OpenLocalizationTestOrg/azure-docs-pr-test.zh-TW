---
title: "適用於 B2B 監視的自訂追蹤結構描述 - Azure Logic Apps | Microsoft Docs"
description: "建立自訂追蹤結構描述以監視來自 Azure 整合帳戶中交易的 B2B 訊息。"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="1f38c-103">啟用追蹤來監視您的完整工作流程，端對端</span><span class="sxs-lookup"><span data-stu-id="1f38c-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="1f38c-104">有內建的追蹤可供您啟用您不同部分的企業對企業工作流程，例如追蹤 AS2 或 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="1f38c-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="1f38c-105">當您建立包含邏輯應用程式、BizTalk Server、SQL Server 或任何其他層級的工作流程時，您可以啟用自訂追蹤，記錄從您工作流程開始到結尾的事件。</span><span class="sxs-lookup"><span data-stu-id="1f38c-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="1f38c-106">本主題提供您可以在邏輯應用程式外部層級中使用的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="1f38c-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="1f38c-107">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="1f38c-107">Custom tracking schema</span></span>
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| <span data-ttu-id="1f38c-108">屬性</span><span class="sxs-lookup"><span data-stu-id="1f38c-108">Property</span></span> | <span data-ttu-id="1f38c-109">類型</span><span class="sxs-lookup"><span data-stu-id="1f38c-109">Type</span></span> | <span data-ttu-id="1f38c-110">說明</span><span class="sxs-lookup"><span data-stu-id="1f38c-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1f38c-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="1f38c-111">sourceType</span></span> |   | <span data-ttu-id="1f38c-112">執行來源的類型。</span><span class="sxs-lookup"><span data-stu-id="1f38c-112">Type of the run source.</span></span> <span data-ttu-id="1f38c-113">允許的值為 **Microsoft.Logic/workflows** 和 **custom**。</span><span class="sxs-lookup"><span data-stu-id="1f38c-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="1f38c-114">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-114">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-115">來源</span><span class="sxs-lookup"><span data-stu-id="1f38c-115">Source</span></span> |   | <span data-ttu-id="1f38c-116">如果來源類型是 **Microsoft.Logic/workflows**，則來源資訊必須遵循此結構描述。</span><span class="sxs-lookup"><span data-stu-id="1f38c-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="1f38c-117">如果來源類型為 **custom**，則結構描述為 JToken。</span><span class="sxs-lookup"><span data-stu-id="1f38c-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="1f38c-118">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-118">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-119">systemId</span><span class="sxs-lookup"><span data-stu-id="1f38c-119">systemId</span></span> | <span data-ttu-id="1f38c-120">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-120">String</span></span> | <span data-ttu-id="1f38c-121">邏輯應用程式系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f38c-121">Logic app system ID.</span></span> <span data-ttu-id="1f38c-122">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-122">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-123">runId</span><span class="sxs-lookup"><span data-stu-id="1f38c-123">runId</span></span> | <span data-ttu-id="1f38c-124">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-124">String</span></span> | <span data-ttu-id="1f38c-125">邏輯應用程式執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f38c-125">Logic app run ID.</span></span> <span data-ttu-id="1f38c-126">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-126">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-127">operationName</span><span class="sxs-lookup"><span data-stu-id="1f38c-127">operationName</span></span> | <span data-ttu-id="1f38c-128">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-128">String</span></span> | <span data-ttu-id="1f38c-129">作業 (例如動作或觸發程序) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1f38c-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="1f38c-130">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-130">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="1f38c-131">repeatItemScopeName</span></span> | <span data-ttu-id="1f38c-132">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-132">String</span></span> | <span data-ttu-id="1f38c-133">如果動作在 `foreach`/`until` 迴圈內，重複項目名稱。</span><span class="sxs-lookup"><span data-stu-id="1f38c-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="1f38c-134">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-134">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="1f38c-135">repeatItemIndex</span></span> | <span data-ttu-id="1f38c-136">Integer</span><span class="sxs-lookup"><span data-stu-id="1f38c-136">Integer</span></span> | <span data-ttu-id="1f38c-137">動作是否在 `foreach`/`until` 迴圈內。</span><span class="sxs-lookup"><span data-stu-id="1f38c-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="1f38c-138">指出重複的項目索引。</span><span class="sxs-lookup"><span data-stu-id="1f38c-138">Indicates the repeated item index.</span></span> <span data-ttu-id="1f38c-139">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-139">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="1f38c-140">trackingId</span></span> | <span data-ttu-id="1f38c-141">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-141">String</span></span> | <span data-ttu-id="1f38c-142">追蹤識別碼，使訊息相互關聯。</span><span class="sxs-lookup"><span data-stu-id="1f38c-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="1f38c-143">(選用)</span><span class="sxs-lookup"><span data-stu-id="1f38c-143">(Optional)</span></span> |
| <span data-ttu-id="1f38c-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="1f38c-144">correlationId</span></span> | <span data-ttu-id="1f38c-145">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-145">String</span></span> | <span data-ttu-id="1f38c-146">相互關連識別碼，使訊息相互關聯。</span><span class="sxs-lookup"><span data-stu-id="1f38c-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="1f38c-147">(選用)</span><span class="sxs-lookup"><span data-stu-id="1f38c-147">(Optional)</span></span> |
| <span data-ttu-id="1f38c-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="1f38c-148">clientRequestId</span></span> | <span data-ttu-id="1f38c-149">String</span><span class="sxs-lookup"><span data-stu-id="1f38c-149">String</span></span> | <span data-ttu-id="1f38c-150">用戶端可以填入此值，使訊息相互關聯。</span><span class="sxs-lookup"><span data-stu-id="1f38c-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="1f38c-151">(選用)</span><span class="sxs-lookup"><span data-stu-id="1f38c-151">(Optional)</span></span> |
| <span data-ttu-id="1f38c-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="1f38c-152">eventLevel</span></span> |   | <span data-ttu-id="1f38c-153">事件的層級。</span><span class="sxs-lookup"><span data-stu-id="1f38c-153">Level of the event.</span></span> <span data-ttu-id="1f38c-154">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-154">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="1f38c-155">eventTime</span></span> |   | <span data-ttu-id="1f38c-156">事件的時間，以 UTC 格式 YYYY-MM-DDTHH:MM:SS.00000Z。</span><span class="sxs-lookup"><span data-stu-id="1f38c-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="1f38c-157">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-157">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-158">recordType</span><span class="sxs-lookup"><span data-stu-id="1f38c-158">recordType</span></span> |   | <span data-ttu-id="1f38c-159">追蹤記錄的類型。</span><span class="sxs-lookup"><span data-stu-id="1f38c-159">Type of the track record.</span></span> <span data-ttu-id="1f38c-160">允許的值為 **custom**。</span><span class="sxs-lookup"><span data-stu-id="1f38c-160">Allowed value is **custom**.</span></span> <span data-ttu-id="1f38c-161">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-161">(Mandatory)</span></span> |
| <span data-ttu-id="1f38c-162">record</span><span class="sxs-lookup"><span data-stu-id="1f38c-162">record</span></span> |   | <span data-ttu-id="1f38c-163">自訂記錄類型。</span><span class="sxs-lookup"><span data-stu-id="1f38c-163">Custom record type.</span></span> <span data-ttu-id="1f38c-164">允許的格式為 JToken。</span><span class="sxs-lookup"><span data-stu-id="1f38c-164">Allowed format is JToken.</span></span> <span data-ttu-id="1f38c-165">(必要)</span><span class="sxs-lookup"><span data-stu-id="1f38c-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="1f38c-166">B2B 通訊協定追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="1f38c-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="1f38c-167">如需 B2B 通訊協定追蹤結構描述的相關資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="1f38c-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="1f38c-168">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="1f38c-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="1f38c-169">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="1f38c-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="1f38c-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f38c-170">Next steps</span></span>
* <span data-ttu-id="1f38c-171">[深入了解監視 B2B 訊息](logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="1f38c-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="1f38c-172">了解[在 Operations Management Suite 入口網站中追蹤 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="1f38c-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="1f38c-173">[深入了解企業整合套件](../logic-apps/logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1f38c-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
