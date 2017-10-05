---
title: "適用於 B2B 監視的 AS2 追蹤結構描述 - Azure Logic Apps | Microsoft Docs"
description: "使用 AS2 追蹤結構描述以監視來自 Azure 整合帳戶中交易的 B2B 訊息。"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 31bd296dc5ed5ac6998a6c05ee80fd38b12d662c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-to-monitor-success-errors-and-message-properties"></a><span data-ttu-id="6a213-103">啟動或啟用追蹤 AS2 訊息和 MDN，以監視成功、錯誤和訊息屬性</span><span class="sxs-lookup"><span data-stu-id="6a213-103">Start or enable tracking of AS2 messages and MDNs to monitor success, errors, and message properties</span></span>
<span data-ttu-id="6a213-104">您可以在 Azure 整合帳戶中使用這些 AS2 追蹤結構描述，協助您監視企業對企業 (B2B) 交易︰</span><span class="sxs-lookup"><span data-stu-id="6a213-104">You can use these AS2 tracking schemas in your Azure integration account to help you monitor business-to-business (B2B) transactions:</span></span>

* <span data-ttu-id="6a213-105">AS2 訊息追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6a213-105">AS2 message tracking schema</span></span>
* <span data-ttu-id="6a213-106">AS2 MDN 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6a213-106">AS2 MDN tracking schema</span></span>

## <a name="as2-message-tracking-schema"></a><span data-ttu-id="6a213-107">AS2 訊息追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6a213-107">AS2 message tracking schema</span></span>
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| <span data-ttu-id="6a213-108">屬性</span><span class="sxs-lookup"><span data-stu-id="6a213-108">Property</span></span> | <span data-ttu-id="6a213-109">類型</span><span class="sxs-lookup"><span data-stu-id="6a213-109">Type</span></span> | <span data-ttu-id="6a213-110">說明</span><span class="sxs-lookup"><span data-stu-id="6a213-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a213-111">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="6a213-111">senderPartnerName</span></span> | <span data-ttu-id="6a213-112">String</span><span class="sxs-lookup"><span data-stu-id="6a213-112">String</span></span> | <span data-ttu-id="6a213-113">AS2 訊息傳送者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-113">AS2 message sender's partner name.</span></span> <span data-ttu-id="6a213-114">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-114">(Optional)</span></span> |
| <span data-ttu-id="6a213-115">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="6a213-115">receiverPartnerName</span></span> | <span data-ttu-id="6a213-116">String</span><span class="sxs-lookup"><span data-stu-id="6a213-116">String</span></span> | <span data-ttu-id="6a213-117">AS2 訊息接收者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-117">AS2 message receiver's partner name.</span></span> <span data-ttu-id="6a213-118">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-118">(Optional)</span></span> |
| <span data-ttu-id="6a213-119">as2To</span><span class="sxs-lookup"><span data-stu-id="6a213-119">as2To</span></span> | <span data-ttu-id="6a213-120">String</span><span class="sxs-lookup"><span data-stu-id="6a213-120">String</span></span> | <span data-ttu-id="6a213-121">AS2 訊息接收者的名稱，從 AS2 訊息的標頭。</span><span class="sxs-lookup"><span data-stu-id="6a213-121">AS2 message receiver’s name, from the headers of the AS2 message.</span></span> <span data-ttu-id="6a213-122">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-122">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-123">as2From</span><span class="sxs-lookup"><span data-stu-id="6a213-123">as2From</span></span> | <span data-ttu-id="6a213-124">String</span><span class="sxs-lookup"><span data-stu-id="6a213-124">String</span></span> | <span data-ttu-id="6a213-125">AS2 訊息傳送者的名稱，從 AS2 訊息的標頭。</span><span class="sxs-lookup"><span data-stu-id="6a213-125">AS2 message sender’s name, from the headers of the AS2 message.</span></span> <span data-ttu-id="6a213-126">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-126">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-127">agreementName</span><span class="sxs-lookup"><span data-stu-id="6a213-127">agreementName</span></span> | <span data-ttu-id="6a213-128">String</span><span class="sxs-lookup"><span data-stu-id="6a213-128">String</span></span> | <span data-ttu-id="6a213-129">據以解析訊息的 AS2 合約名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-129">Name of the AS2 agreement to which the messages are resolved.</span></span> <span data-ttu-id="6a213-130">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-130">(Optional)</span></span> |
| <span data-ttu-id="6a213-131">direction</span><span class="sxs-lookup"><span data-stu-id="6a213-131">direction</span></span> | <span data-ttu-id="6a213-132">String</span><span class="sxs-lookup"><span data-stu-id="6a213-132">String</span></span> | <span data-ttu-id="6a213-133">訊息流程的方向，接收或傳送。</span><span class="sxs-lookup"><span data-stu-id="6a213-133">Direction of the message flow, receive or send.</span></span> <span data-ttu-id="6a213-134">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-134">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-135">messageId</span><span class="sxs-lookup"><span data-stu-id="6a213-135">messageId</span></span> | <span data-ttu-id="6a213-136">String</span><span class="sxs-lookup"><span data-stu-id="6a213-136">String</span></span> | <span data-ttu-id="6a213-137">AS2 訊息 ID，從 AS2 訊息的標頭 (選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-137">AS2 message ID, from the headers of the AS2 message (Optional)</span></span> |
| <span data-ttu-id="6a213-138">dispositionType</span><span class="sxs-lookup"><span data-stu-id="6a213-138">dispositionType</span></span> |<span data-ttu-id="6a213-139">String</span><span class="sxs-lookup"><span data-stu-id="6a213-139">String</span></span> | <span data-ttu-id="6a213-140">訊息處理通知 (MDN) 配置類型值。</span><span class="sxs-lookup"><span data-stu-id="6a213-140">Message Disposition Notification (MDN) disposition type value.</span></span> <span data-ttu-id="6a213-141">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-141">(Optional)</span></span> |
| <span data-ttu-id="6a213-142">fileName</span><span class="sxs-lookup"><span data-stu-id="6a213-142">fileName</span></span> | <span data-ttu-id="6a213-143">String</span><span class="sxs-lookup"><span data-stu-id="6a213-143">String</span></span> | <span data-ttu-id="6a213-144">檔案名稱，從 AS2 訊息的標頭。</span><span class="sxs-lookup"><span data-stu-id="6a213-144">File name, from the header of the AS2 message.</span></span> <span data-ttu-id="6a213-145">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-145">(Optional)</span></span> |
| <span data-ttu-id="6a213-146">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="6a213-146">isMessageFailed</span></span> |<span data-ttu-id="6a213-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-147">Boolean</span></span> | <span data-ttu-id="6a213-148">AS2 訊息是否失敗。</span><span class="sxs-lookup"><span data-stu-id="6a213-148">Whether the AS2 message failed.</span></span> <span data-ttu-id="6a213-149">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-149">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-150">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="6a213-150">isMessageSigned</span></span> | <span data-ttu-id="6a213-151">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-151">Boolean</span></span> | <span data-ttu-id="6a213-152">AS2 訊息是否簽署。</span><span class="sxs-lookup"><span data-stu-id="6a213-152">Whether the AS2 message was signed.</span></span> <span data-ttu-id="6a213-153">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-153">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-154">isMessageEncrypted</span><span class="sxs-lookup"><span data-stu-id="6a213-154">isMessageEncrypted</span></span> | <span data-ttu-id="6a213-155">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-155">Boolean</span></span> | <span data-ttu-id="6a213-156">AS2 訊息是否加密。</span><span class="sxs-lookup"><span data-stu-id="6a213-156">Whether the AS2 message was encrypted.</span></span> <span data-ttu-id="6a213-157">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-157">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-158">isMessageCompressed</span><span class="sxs-lookup"><span data-stu-id="6a213-158">isMessageCompressed</span></span> |<span data-ttu-id="6a213-159">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-159">Boolean</span></span> | <span data-ttu-id="6a213-160">AS2 訊息是否壓縮。</span><span class="sxs-lookup"><span data-stu-id="6a213-160">Whether the AS2 message was compressed.</span></span> <span data-ttu-id="6a213-161">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-161">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-162">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="6a213-162">correlationMessageId</span></span> | <span data-ttu-id="6a213-163">String</span><span class="sxs-lookup"><span data-stu-id="6a213-163">String</span></span> | <span data-ttu-id="6a213-164">AS2 訊息識別碼，將訊息與 MDN 相互關聯。</span><span class="sxs-lookup"><span data-stu-id="6a213-164">AS2 message ID, to correlate messages with MDNs.</span></span> <span data-ttu-id="6a213-165">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-165">(Optional)</span></span> |
| <span data-ttu-id="6a213-166">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="6a213-166">incomingHeaders</span></span> |<span data-ttu-id="6a213-167">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="6a213-167">Dictionary of JToken</span></span> | <span data-ttu-id="6a213-168">內送 AS2 訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a213-168">Incoming AS2 message header details.</span></span> <span data-ttu-id="6a213-169">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-169">(Optional)</span></span> |
| <span data-ttu-id="6a213-170">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="6a213-170">outgoingHeaders</span></span> |<span data-ttu-id="6a213-171">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="6a213-171">Dictionary of JToken</span></span> | <span data-ttu-id="6a213-172">外寄 AS2 訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a213-172">Outgoing AS2 message header details.</span></span> <span data-ttu-id="6a213-173">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-173">(Optional)</span></span> |
| <span data-ttu-id="6a213-174">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="6a213-174">isNrrEnabled</span></span> | <span data-ttu-id="6a213-175">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-175">Boolean</span></span> | <span data-ttu-id="6a213-176">如果不知道值，則使用預設值。</span><span class="sxs-lookup"><span data-stu-id="6a213-176">Use default value if the value is not known.</span></span> <span data-ttu-id="6a213-177">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-177">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-178">isMdnExpected</span><span class="sxs-lookup"><span data-stu-id="6a213-178">isMdnExpected</span></span> | <span data-ttu-id="6a213-179">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-179">Boolean</span></span> | <span data-ttu-id="6a213-180">如果不知道值，則使用預設值。</span><span class="sxs-lookup"><span data-stu-id="6a213-180">Use default value if the value is not known.</span></span> <span data-ttu-id="6a213-181">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-181">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-182">mdnType</span><span class="sxs-lookup"><span data-stu-id="6a213-182">mdnType</span></span> | <span data-ttu-id="6a213-183">例舉</span><span class="sxs-lookup"><span data-stu-id="6a213-183">Enum</span></span> | <span data-ttu-id="6a213-184">允許的值為 **NotConfigured**、**Sync** 和 **Async**。</span><span class="sxs-lookup"><span data-stu-id="6a213-184">Allowed values are **NotConfigured**, **Sync**, and **Async**.</span></span> <span data-ttu-id="6a213-185">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-185">(Mandatory)</span></span> |

## <a name="as2-mdn-tracking-schema"></a><span data-ttu-id="6a213-186">AS2 MDN 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="6a213-186">AS2 MDN tracking schema</span></span>
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| <span data-ttu-id="6a213-187">屬性</span><span class="sxs-lookup"><span data-stu-id="6a213-187">Property</span></span> | <span data-ttu-id="6a213-188">類型</span><span class="sxs-lookup"><span data-stu-id="6a213-188">Type</span></span> | <span data-ttu-id="6a213-189">說明</span><span class="sxs-lookup"><span data-stu-id="6a213-189">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6a213-190">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="6a213-190">senderPartnerName</span></span> | <span data-ttu-id="6a213-191">String</span><span class="sxs-lookup"><span data-stu-id="6a213-191">String</span></span> | <span data-ttu-id="6a213-192">AS2 訊息傳送者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-192">AS2 message sender's partner name.</span></span> <span data-ttu-id="6a213-193">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-193">(Optional)</span></span> |
| <span data-ttu-id="6a213-194">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="6a213-194">receiverPartnerName</span></span> | <span data-ttu-id="6a213-195">String</span><span class="sxs-lookup"><span data-stu-id="6a213-195">String</span></span> | <span data-ttu-id="6a213-196">AS2 訊息接收者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-196">AS2 message receiver's partner name.</span></span> <span data-ttu-id="6a213-197">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-197">(Optional)</span></span> |
| <span data-ttu-id="6a213-198">as2To</span><span class="sxs-lookup"><span data-stu-id="6a213-198">as2To</span></span> | <span data-ttu-id="6a213-199">String</span><span class="sxs-lookup"><span data-stu-id="6a213-199">String</span></span> | <span data-ttu-id="6a213-200">接收該 AS2 訊息的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-200">Partner name who receives the AS2 message.</span></span> <span data-ttu-id="6a213-201">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-201">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-202">as2From</span><span class="sxs-lookup"><span data-stu-id="6a213-202">as2From</span></span> | <span data-ttu-id="6a213-203">String</span><span class="sxs-lookup"><span data-stu-id="6a213-203">String</span></span> | <span data-ttu-id="6a213-204">傳送該 AS2 訊息的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-204">Partner name who sends the AS2 message.</span></span> <span data-ttu-id="6a213-205">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-205">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-206">agreementName</span><span class="sxs-lookup"><span data-stu-id="6a213-206">agreementName</span></span> | <span data-ttu-id="6a213-207">String</span><span class="sxs-lookup"><span data-stu-id="6a213-207">String</span></span> | <span data-ttu-id="6a213-208">據以解析訊息的 AS2 合約名稱。</span><span class="sxs-lookup"><span data-stu-id="6a213-208">Name of the AS2 agreement to which the messages are resolved.</span></span> <span data-ttu-id="6a213-209">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-209">(Optional)</span></span> |
| <span data-ttu-id="6a213-210">direction</span><span class="sxs-lookup"><span data-stu-id="6a213-210">direction</span></span> |<span data-ttu-id="6a213-211">String</span><span class="sxs-lookup"><span data-stu-id="6a213-211">String</span></span> | <span data-ttu-id="6a213-212">訊息流程的方向，接收或傳送。</span><span class="sxs-lookup"><span data-stu-id="6a213-212">Direction of the message flow, receive or send.</span></span> <span data-ttu-id="6a213-213">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-213">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-214">messageId</span><span class="sxs-lookup"><span data-stu-id="6a213-214">messageId</span></span> | <span data-ttu-id="6a213-215">String</span><span class="sxs-lookup"><span data-stu-id="6a213-215">String</span></span> | <span data-ttu-id="6a213-216">AS2 訊息識別碼。</span><span class="sxs-lookup"><span data-stu-id="6a213-216">AS2 message ID.</span></span> <span data-ttu-id="6a213-217">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-217">(Optional)</span></span> |
| <span data-ttu-id="6a213-218">originalMessageId</span><span class="sxs-lookup"><span data-stu-id="6a213-218">originalMessageId</span></span> |<span data-ttu-id="6a213-219">String</span><span class="sxs-lookup"><span data-stu-id="6a213-219">String</span></span> | <span data-ttu-id="6a213-220">AS2 原始訊息識別碼。</span><span class="sxs-lookup"><span data-stu-id="6a213-220">AS2 original message ID.</span></span> <span data-ttu-id="6a213-221">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-221">(Optional)</span></span> |
| <span data-ttu-id="6a213-222">dispositionType</span><span class="sxs-lookup"><span data-stu-id="6a213-222">dispositionType</span></span> | <span data-ttu-id="6a213-223">String</span><span class="sxs-lookup"><span data-stu-id="6a213-223">String</span></span> | <span data-ttu-id="6a213-224">MDN 處置類型值。</span><span class="sxs-lookup"><span data-stu-id="6a213-224">MDN disposition type value.</span></span> <span data-ttu-id="6a213-225">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-225">(Optional)</span></span> |
| <span data-ttu-id="6a213-226">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="6a213-226">isMessageFailed</span></span> |<span data-ttu-id="6a213-227">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-227">Boolean</span></span> | <span data-ttu-id="6a213-228">AS2 訊息是否失敗。</span><span class="sxs-lookup"><span data-stu-id="6a213-228">Whether the AS2 message failed.</span></span> <span data-ttu-id="6a213-229">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-229">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-230">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="6a213-230">isMessageSigned</span></span> |<span data-ttu-id="6a213-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-231">Boolean</span></span> | <span data-ttu-id="6a213-232">AS2 訊息是否簽署。</span><span class="sxs-lookup"><span data-stu-id="6a213-232">Whether the AS2 message was signed.</span></span> <span data-ttu-id="6a213-233">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-233">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-234">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="6a213-234">isNrrEnabled</span></span> | <span data-ttu-id="6a213-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="6a213-235">Boolean</span></span> | <span data-ttu-id="6a213-236">如果不知道值，則使用預設值。</span><span class="sxs-lookup"><span data-stu-id="6a213-236">Use default value if the value is not known.</span></span> <span data-ttu-id="6a213-237">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-237">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-238">StatusCode</span><span class="sxs-lookup"><span data-stu-id="6a213-238">statusCode</span></span> | <span data-ttu-id="6a213-239">例舉</span><span class="sxs-lookup"><span data-stu-id="6a213-239">Enum</span></span> | <span data-ttu-id="6a213-240">允許的值為 **Accepted**、**Rejected** 和 **AcceptedWithErrors**。</span><span class="sxs-lookup"><span data-stu-id="6a213-240">Allowed values are **Accepted**, **Rejected**, and **AcceptedWithErrors**.</span></span> <span data-ttu-id="6a213-241">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-241">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-242">micVerificationStatus</span><span class="sxs-lookup"><span data-stu-id="6a213-242">micVerificationStatus</span></span> | <span data-ttu-id="6a213-243">例舉</span><span class="sxs-lookup"><span data-stu-id="6a213-243">Enum</span></span> | <span data-ttu-id="6a213-244">允許的值為 **NotApplicable**、**Succeeded** 和 **Failed**。</span><span class="sxs-lookup"><span data-stu-id="6a213-244">Allowed values are **NotApplicable**, **Succeeded**, and **Failed**.</span></span> <span data-ttu-id="6a213-245">(必要)</span><span class="sxs-lookup"><span data-stu-id="6a213-245">(Mandatory)</span></span> |
| <span data-ttu-id="6a213-246">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="6a213-246">correlationMessageId</span></span> | <span data-ttu-id="6a213-247">String</span><span class="sxs-lookup"><span data-stu-id="6a213-247">String</span></span> | <span data-ttu-id="6a213-248">相互關連識別碼。</span><span class="sxs-lookup"><span data-stu-id="6a213-248">Correlation ID.</span></span> <span data-ttu-id="6a213-249">原始 messaged 識別碼 (設定 MDN 之訊息的訊息識別碼)。</span><span class="sxs-lookup"><span data-stu-id="6a213-249">The original messaged ID (the message ID of the message for which MDN is configured).</span></span> <span data-ttu-id="6a213-250">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-250">(Optional)</span></span> |
| <span data-ttu-id="6a213-251">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="6a213-251">incomingHeaders</span></span> | <span data-ttu-id="6a213-252">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="6a213-252">Dictionary of JToken</span></span> | <span data-ttu-id="6a213-253">指出內送訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a213-253">Indicates incoming message header details.</span></span> <span data-ttu-id="6a213-254">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-254">(Optional)</span></span> |
| <span data-ttu-id="6a213-255">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="6a213-255">outgoingHeaders</span></span> |<span data-ttu-id="6a213-256">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="6a213-256">Dictionary of JToken</span></span> | <span data-ttu-id="6a213-257">指出外寄訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6a213-257">Indicates outgoing message header details.</span></span> <span data-ttu-id="6a213-258">(選用)</span><span class="sxs-lookup"><span data-stu-id="6a213-258">(Optional)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6a213-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a213-259">Next steps</span></span>
* <span data-ttu-id="6a213-260">[深入了解企業整合套件](../logic-apps/logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6a213-260">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>    
* <span data-ttu-id="6a213-261">[深入了解監視 B2B 訊息](logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="6a213-261">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="6a213-262">[深入了解 B2B 自訂追蹤結構描述](logic-apps-track-integration-account-custom-tracking-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="6a213-262">Learn more about [B2B custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span></span>   
* <span data-ttu-id="6a213-263">深入了解 [X12 追蹤結構描述](logic-apps-track-integration-account-x12-tracking-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="6a213-263">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span></span>   
* <span data-ttu-id="6a213-264">了解[在 Operations Management Suite 入口網站中追蹤 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="6a213-264">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
