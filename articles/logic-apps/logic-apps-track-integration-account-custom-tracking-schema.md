---
title: "追蹤結構描述 b2b aaaCustom 監視-Azure 邏輯應用程式 |Microsoft 文件"
description: "建立自訂追蹤結構描述 toomonitor B2B 訊息從您的 Azure 整合帳戶中的交易。"
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
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="6c667-103">讓您完成的工作流程，端對端追蹤 toomonitor</span><span class="sxs-lookup"><span data-stu-id="6c667-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="6c667-104">有內建的追蹤可供您啟用您不同部分的企業對企業工作流程，例如追蹤 AS2 或 X12 訊息。</span><span class="sxs-lookup"><span data-stu-id="6c667-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="6c667-105">當您建立包含邏輯應用程式、 BizTalk Server、 SQL Server 或任何其他層級的工作流程時，您可以啟用自訂的追蹤記錄的事件，從您的工作流程 hello 開頭 toohello 結尾。</span><span class="sxs-lookup"><span data-stu-id="6c667-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="6c667-106">本主題提供您可以使用 hello 層級中，外部應用程式邏輯的自訂程式碼。</span><span class="sxs-lookup"><span data-stu-id="6c667-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="6c667-107">自訂追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6c667-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="6c667-108">屬性</span><span class="sxs-lookup"><span data-stu-id="6c667-108">Property</span></span> | <span data-ttu-id="6c667-109">類型</span><span class="sxs-lookup"><span data-stu-id="6c667-109">Type</span></span> | <span data-ttu-id="6c667-110">說明</span><span class="sxs-lookup"><span data-stu-id="6c667-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6c667-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="6c667-111">sourceType</span></span> |   | <span data-ttu-id="6c667-112">Hello 執行來源的類型。</span><span class="sxs-lookup"><span data-stu-id="6c667-112">Type of hello run source.</span></span> <span data-ttu-id="6c667-113">允許的值為 **Microsoft.Logic/workflows** 和 **custom**。</span><span class="sxs-lookup"><span data-stu-id="6c667-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="6c667-114">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-114">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-115">來源</span><span class="sxs-lookup"><span data-stu-id="6c667-115">Source</span></span> |   | <span data-ttu-id="6c667-116">如果 hello 來源類型為**Microsoft.Logic/workflows**，hello 來源資訊需要 toofollow 這個結構描述。</span><span class="sxs-lookup"><span data-stu-id="6c667-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="6c667-117">如果 hello 來源類型為**自訂**，hello 結構描述是 JToken。</span><span class="sxs-lookup"><span data-stu-id="6c667-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="6c667-118">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-118">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-119">systemId</span><span class="sxs-lookup"><span data-stu-id="6c667-119">systemId</span></span> | <span data-ttu-id="6c667-120">String</span><span class="sxs-lookup"><span data-stu-id="6c667-120">String</span></span> | <span data-ttu-id="6c667-121">邏輯應用程式系統識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c667-121">Logic app system ID.</span></span> <span data-ttu-id="6c667-122">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-122">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-123">runId</span><span class="sxs-lookup"><span data-stu-id="6c667-123">runId</span></span> | <span data-ttu-id="6c667-124">String</span><span class="sxs-lookup"><span data-stu-id="6c667-124">String</span></span> | <span data-ttu-id="6c667-125">邏輯應用程式執行識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c667-125">Logic app run ID.</span></span> <span data-ttu-id="6c667-126">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-126">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-127">operationName</span><span class="sxs-lookup"><span data-stu-id="6c667-127">operationName</span></span> | <span data-ttu-id="6c667-128">String</span><span class="sxs-lookup"><span data-stu-id="6c667-128">String</span></span> | <span data-ttu-id="6c667-129">Hello 作業 （例如，動作或觸發程序） 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6c667-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="6c667-130">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-130">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="6c667-131">repeatItemScopeName</span></span> | <span data-ttu-id="6c667-132">String</span><span class="sxs-lookup"><span data-stu-id="6c667-132">String</span></span> | <span data-ttu-id="6c667-133">如果 hello 動作內重複項目名稱`foreach` / `until`迴圈。</span><span class="sxs-lookup"><span data-stu-id="6c667-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="6c667-134">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-134">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="6c667-135">repeatItemIndex</span></span> | <span data-ttu-id="6c667-136">Integer</span><span class="sxs-lookup"><span data-stu-id="6c667-136">Integer</span></span> | <span data-ttu-id="6c667-137">Hello 動作是否內`foreach` / `until`迴圈。</span><span class="sxs-lookup"><span data-stu-id="6c667-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="6c667-138">指出 hello 重複的項目索引。</span><span class="sxs-lookup"><span data-stu-id="6c667-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="6c667-139">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-139">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="6c667-140">trackingId</span></span> | <span data-ttu-id="6c667-141">String</span><span class="sxs-lookup"><span data-stu-id="6c667-141">String</span></span> | <span data-ttu-id="6c667-142">Toocorrelate hello 訊息追蹤識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c667-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="6c667-143">(選用)</span><span class="sxs-lookup"><span data-stu-id="6c667-143">(Optional)</span></span> |
| <span data-ttu-id="6c667-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="6c667-144">correlationId</span></span> | <span data-ttu-id="6c667-145">String</span><span class="sxs-lookup"><span data-stu-id="6c667-145">String</span></span> | <span data-ttu-id="6c667-146">Toocorrelate hello 訊息相互關聯識別碼。</span><span class="sxs-lookup"><span data-stu-id="6c667-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="6c667-147">(選用)</span><span class="sxs-lookup"><span data-stu-id="6c667-147">(Optional)</span></span> |
| <span data-ttu-id="6c667-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="6c667-148">clientRequestId</span></span> | <span data-ttu-id="6c667-149">String</span><span class="sxs-lookup"><span data-stu-id="6c667-149">String</span></span> | <span data-ttu-id="6c667-150">用戶端可以將它填入 toocorrelate 訊息。</span><span class="sxs-lookup"><span data-stu-id="6c667-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="6c667-151">(選用)</span><span class="sxs-lookup"><span data-stu-id="6c667-151">(Optional)</span></span> |
| <span data-ttu-id="6c667-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="6c667-152">eventLevel</span></span> |   | <span data-ttu-id="6c667-153">Hello 事件層級。</span><span class="sxs-lookup"><span data-stu-id="6c667-153">Level of hello event.</span></span> <span data-ttu-id="6c667-154">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-154">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="6c667-155">eventTime</span></span> |   | <span data-ttu-id="6c667-156">以 UTC 格式 YYYY-MM-DDTHH:MM:SS.00000Z hello 事件的時間。</span><span class="sxs-lookup"><span data-stu-id="6c667-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="6c667-157">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-157">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-158">recordType</span><span class="sxs-lookup"><span data-stu-id="6c667-158">recordType</span></span> |   | <span data-ttu-id="6c667-159">Hello 追蹤記錄的類型。</span><span class="sxs-lookup"><span data-stu-id="6c667-159">Type of hello track record.</span></span> <span data-ttu-id="6c667-160">允許的值為 **custom**。</span><span class="sxs-lookup"><span data-stu-id="6c667-160">Allowed value is **custom**.</span></span> <span data-ttu-id="6c667-161">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-161">(Mandatory)</span></span> |
| <span data-ttu-id="6c667-162">record</span><span class="sxs-lookup"><span data-stu-id="6c667-162">record</span></span> |   | <span data-ttu-id="6c667-163">自訂記錄類型。</span><span class="sxs-lookup"><span data-stu-id="6c667-163">Custom record type.</span></span> <span data-ttu-id="6c667-164">允許的格式為 JToken。</span><span class="sxs-lookup"><span data-stu-id="6c667-164">Allowed format is JToken.</span></span> <span data-ttu-id="6c667-165">(必要)</span><span class="sxs-lookup"><span data-stu-id="6c667-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="6c667-166">B2B 通訊協定追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6c667-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="6c667-167">如需 B2B 通訊協定追蹤結構描述的相關資訊，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="6c667-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="6c667-168">AS2 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6c667-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="6c667-169">X12 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6c667-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="6c667-170">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c667-170">Next steps</span></span>
* <span data-ttu-id="6c667-171">[深入了解監視 B2B 訊息](logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="6c667-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="6c667-172">深入了解[追蹤 hello Operations Management Suite 入口網站中的 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="6c667-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="6c667-173">深入了解 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6c667-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
