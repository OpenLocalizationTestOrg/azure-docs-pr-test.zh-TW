---
title: "aaaAS2 追蹤結構描述 B2B 監視-Azure 邏輯應用程式 |Microsoft 文件"
description: "使用 AS2 追蹤結構描述 toomonitor B2B 訊息從您的 Azure 整合帳戶中的交易。"
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
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a><span data-ttu-id="0f66f-103">啟動或啟用的 AS2 訊息和 Mdn toomonitor 成功、 錯誤和訊息屬性追蹤</span><span class="sxs-lookup"><span data-stu-id="0f66f-103">Start or enable tracking of AS2 messages and MDNs toomonitor success, errors, and message properties</span></span>
<span data-ttu-id="0f66f-104">您可以使用這些 AS2 追蹤結構描述您可以在您的 Azure 整合帳戶 toohelp 監視企業對企業 (B2B) 交易：</span><span class="sxs-lookup"><span data-stu-id="0f66f-104">You can use these AS2 tracking schemas in your Azure integration account toohelp you monitor business-to-business (B2B) transactions:</span></span>

* <span data-ttu-id="0f66f-105">AS2 訊息追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="0f66f-105">AS2 message tracking schema</span></span>
* <span data-ttu-id="0f66f-106">AS2 MDN 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="0f66f-106">AS2 MDN tracking schema</span></span>

## <a name="as2-message-tracking-schema"></a><span data-ttu-id="0f66f-107">AS2 訊息追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="0f66f-107">AS2 message tracking schema</span></span>
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

| <span data-ttu-id="0f66f-108">屬性</span><span class="sxs-lookup"><span data-stu-id="0f66f-108">Property</span></span> | <span data-ttu-id="0f66f-109">類型</span><span class="sxs-lookup"><span data-stu-id="0f66f-109">Type</span></span> | <span data-ttu-id="0f66f-110">說明</span><span class="sxs-lookup"><span data-stu-id="0f66f-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f66f-111">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="0f66f-111">senderPartnerName</span></span> | <span data-ttu-id="0f66f-112">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-112">String</span></span> | <span data-ttu-id="0f66f-113">AS2 訊息傳送者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-113">AS2 message sender's partner name.</span></span> <span data-ttu-id="0f66f-114">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-114">(Optional)</span></span> |
| <span data-ttu-id="0f66f-115">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="0f66f-115">receiverPartnerName</span></span> | <span data-ttu-id="0f66f-116">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-116">String</span></span> | <span data-ttu-id="0f66f-117">AS2 訊息接收者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-117">AS2 message receiver's partner name.</span></span> <span data-ttu-id="0f66f-118">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-118">(Optional)</span></span> |
| <span data-ttu-id="0f66f-119">as2To</span><span class="sxs-lookup"><span data-stu-id="0f66f-119">as2To</span></span> | <span data-ttu-id="0f66f-120">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-120">String</span></span> | <span data-ttu-id="0f66f-121">AS2 訊息接收者的名稱，從 hello hello AS2 訊息標頭。</span><span class="sxs-lookup"><span data-stu-id="0f66f-121">AS2 message receiver’s name, from hello headers of hello AS2 message.</span></span> <span data-ttu-id="0f66f-122">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-122">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-123">as2From</span><span class="sxs-lookup"><span data-stu-id="0f66f-123">as2From</span></span> | <span data-ttu-id="0f66f-124">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-124">String</span></span> | <span data-ttu-id="0f66f-125">AS2 訊息傳送者的名稱，從 hello hello AS2 訊息標頭。</span><span class="sxs-lookup"><span data-stu-id="0f66f-125">AS2 message sender’s name, from hello headers of hello AS2 message.</span></span> <span data-ttu-id="0f66f-126">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-126">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-127">agreementName</span><span class="sxs-lookup"><span data-stu-id="0f66f-127">agreementName</span></span> | <span data-ttu-id="0f66f-128">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-128">String</span></span> | <span data-ttu-id="0f66f-129">所解析的 hello AS2 協議 toowhich hello 訊息名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-129">Name of hello AS2 agreement toowhich hello messages are resolved.</span></span> <span data-ttu-id="0f66f-130">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-130">(Optional)</span></span> |
| <span data-ttu-id="0f66f-131">direction</span><span class="sxs-lookup"><span data-stu-id="0f66f-131">direction</span></span> | <span data-ttu-id="0f66f-132">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-132">String</span></span> | <span data-ttu-id="0f66f-133">方向 hello 訊息流程、 接收或傳送。</span><span class="sxs-lookup"><span data-stu-id="0f66f-133">Direction of hello message flow, receive or send.</span></span> <span data-ttu-id="0f66f-134">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-134">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-135">messageId</span><span class="sxs-lookup"><span data-stu-id="0f66f-135">messageId</span></span> | <span data-ttu-id="0f66f-136">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-136">String</span></span> | <span data-ttu-id="0f66f-137">AS2 訊息識別碼，從 hello 標頭的 hello AS2 訊息 （選擇性）</span><span class="sxs-lookup"><span data-stu-id="0f66f-137">AS2 message ID, from hello headers of hello AS2 message (Optional)</span></span> |
| <span data-ttu-id="0f66f-138">dispositionType</span><span class="sxs-lookup"><span data-stu-id="0f66f-138">dispositionType</span></span> |<span data-ttu-id="0f66f-139">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-139">String</span></span> | <span data-ttu-id="0f66f-140">訊息處理通知 (MDN) 配置類型值。</span><span class="sxs-lookup"><span data-stu-id="0f66f-140">Message Disposition Notification (MDN) disposition type value.</span></span> <span data-ttu-id="0f66f-141">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-141">(Optional)</span></span> |
| <span data-ttu-id="0f66f-142">fileName</span><span class="sxs-lookup"><span data-stu-id="0f66f-142">fileName</span></span> | <span data-ttu-id="0f66f-143">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-143">String</span></span> | <span data-ttu-id="0f66f-144">檔案名稱，從 hello hello AS2 訊息標頭。</span><span class="sxs-lookup"><span data-stu-id="0f66f-144">File name, from hello header of hello AS2 message.</span></span> <span data-ttu-id="0f66f-145">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-145">(Optional)</span></span> |
| <span data-ttu-id="0f66f-146">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="0f66f-146">isMessageFailed</span></span> |<span data-ttu-id="0f66f-147">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-147">Boolean</span></span> | <span data-ttu-id="0f66f-148">Hello AS2 訊息是否失敗。</span><span class="sxs-lookup"><span data-stu-id="0f66f-148">Whether hello AS2 message failed.</span></span> <span data-ttu-id="0f66f-149">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-149">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-150">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="0f66f-150">isMessageSigned</span></span> | <span data-ttu-id="0f66f-151">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-151">Boolean</span></span> | <span data-ttu-id="0f66f-152">Hello AS2 訊息是否簽署。</span><span class="sxs-lookup"><span data-stu-id="0f66f-152">Whether hello AS2 message was signed.</span></span> <span data-ttu-id="0f66f-153">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-153">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-154">isMessageEncrypted</span><span class="sxs-lookup"><span data-stu-id="0f66f-154">isMessageEncrypted</span></span> | <span data-ttu-id="0f66f-155">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-155">Boolean</span></span> | <span data-ttu-id="0f66f-156">是否已加密 hello AS2 訊息。</span><span class="sxs-lookup"><span data-stu-id="0f66f-156">Whether hello AS2 message was encrypted.</span></span> <span data-ttu-id="0f66f-157">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-157">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-158">isMessageCompressed</span><span class="sxs-lookup"><span data-stu-id="0f66f-158">isMessageCompressed</span></span> |<span data-ttu-id="0f66f-159">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-159">Boolean</span></span> | <span data-ttu-id="0f66f-160">是否 hello AS2 訊息已壓縮。</span><span class="sxs-lookup"><span data-stu-id="0f66f-160">Whether hello AS2 message was compressed.</span></span> <span data-ttu-id="0f66f-161">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-161">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-162">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="0f66f-162">correlationMessageId</span></span> | <span data-ttu-id="0f66f-163">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-163">String</span></span> | <span data-ttu-id="0f66f-164">AS2 訊息識別碼、 toocorrelate Mdn 訊息。</span><span class="sxs-lookup"><span data-stu-id="0f66f-164">AS2 message ID, toocorrelate messages with MDNs.</span></span> <span data-ttu-id="0f66f-165">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-165">(Optional)</span></span> |
| <span data-ttu-id="0f66f-166">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="0f66f-166">incomingHeaders</span></span> |<span data-ttu-id="0f66f-167">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="0f66f-167">Dictionary of JToken</span></span> | <span data-ttu-id="0f66f-168">內送 AS2 訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f66f-168">Incoming AS2 message header details.</span></span> <span data-ttu-id="0f66f-169">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-169">(Optional)</span></span> |
| <span data-ttu-id="0f66f-170">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="0f66f-170">outgoingHeaders</span></span> |<span data-ttu-id="0f66f-171">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="0f66f-171">Dictionary of JToken</span></span> | <span data-ttu-id="0f66f-172">外寄 AS2 訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f66f-172">Outgoing AS2 message header details.</span></span> <span data-ttu-id="0f66f-173">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-173">(Optional)</span></span> |
| <span data-ttu-id="0f66f-174">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="0f66f-174">isNrrEnabled</span></span> | <span data-ttu-id="0f66f-175">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-175">Boolean</span></span> | <span data-ttu-id="0f66f-176">如果不知道 hello 值，請使用預設值。</span><span class="sxs-lookup"><span data-stu-id="0f66f-176">Use default value if hello value is not known.</span></span> <span data-ttu-id="0f66f-177">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-177">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-178">isMdnExpected</span><span class="sxs-lookup"><span data-stu-id="0f66f-178">isMdnExpected</span></span> | <span data-ttu-id="0f66f-179">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-179">Boolean</span></span> | <span data-ttu-id="0f66f-180">如果不知道 hello 值，請使用預設值。</span><span class="sxs-lookup"><span data-stu-id="0f66f-180">Use default value if hello value is not known.</span></span> <span data-ttu-id="0f66f-181">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-181">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-182">mdnType</span><span class="sxs-lookup"><span data-stu-id="0f66f-182">mdnType</span></span> | <span data-ttu-id="0f66f-183">例舉</span><span class="sxs-lookup"><span data-stu-id="0f66f-183">Enum</span></span> | <span data-ttu-id="0f66f-184">允許的值為 **NotConfigured**、**Sync** 和 **Async**。</span><span class="sxs-lookup"><span data-stu-id="0f66f-184">Allowed values are **NotConfigured**, **Sync**, and **Async**.</span></span> <span data-ttu-id="0f66f-185">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-185">(Mandatory)</span></span> |

## <a name="as2-mdn-tracking-schema"></a><span data-ttu-id="0f66f-186">AS2 MDN 追蹤結構描述</span><span class="sxs-lookup"><span data-stu-id="0f66f-186">AS2 MDN tracking schema</span></span>
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

| <span data-ttu-id="0f66f-187">屬性</span><span class="sxs-lookup"><span data-stu-id="0f66f-187">Property</span></span> | <span data-ttu-id="0f66f-188">類型</span><span class="sxs-lookup"><span data-stu-id="0f66f-188">Type</span></span> | <span data-ttu-id="0f66f-189">說明</span><span class="sxs-lookup"><span data-stu-id="0f66f-189">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0f66f-190">senderPartnerName</span><span class="sxs-lookup"><span data-stu-id="0f66f-190">senderPartnerName</span></span> | <span data-ttu-id="0f66f-191">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-191">String</span></span> | <span data-ttu-id="0f66f-192">AS2 訊息傳送者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-192">AS2 message sender's partner name.</span></span> <span data-ttu-id="0f66f-193">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-193">(Optional)</span></span> |
| <span data-ttu-id="0f66f-194">receiverPartnerName</span><span class="sxs-lookup"><span data-stu-id="0f66f-194">receiverPartnerName</span></span> | <span data-ttu-id="0f66f-195">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-195">String</span></span> | <span data-ttu-id="0f66f-196">AS2 訊息接收者的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-196">AS2 message receiver's partner name.</span></span> <span data-ttu-id="0f66f-197">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-197">(Optional)</span></span> |
| <span data-ttu-id="0f66f-198">as2To</span><span class="sxs-lookup"><span data-stu-id="0f66f-198">as2To</span></span> | <span data-ttu-id="0f66f-199">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-199">String</span></span> | <span data-ttu-id="0f66f-200">收到 hello AS2 訊息的夥伴名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-200">Partner name who receives hello AS2 message.</span></span> <span data-ttu-id="0f66f-201">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-201">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-202">as2From</span><span class="sxs-lookup"><span data-stu-id="0f66f-202">as2From</span></span> | <span data-ttu-id="0f66f-203">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-203">String</span></span> | <span data-ttu-id="0f66f-204">夥伴傳送嗨 AS2 訊息的人員名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-204">Partner name who sends hello AS2 message.</span></span> <span data-ttu-id="0f66f-205">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-205">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-206">agreementName</span><span class="sxs-lookup"><span data-stu-id="0f66f-206">agreementName</span></span> | <span data-ttu-id="0f66f-207">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-207">String</span></span> | <span data-ttu-id="0f66f-208">所解析的 hello AS2 協議 toowhich hello 訊息名稱。</span><span class="sxs-lookup"><span data-stu-id="0f66f-208">Name of hello AS2 agreement toowhich hello messages are resolved.</span></span> <span data-ttu-id="0f66f-209">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-209">(Optional)</span></span> |
| <span data-ttu-id="0f66f-210">direction</span><span class="sxs-lookup"><span data-stu-id="0f66f-210">direction</span></span> |<span data-ttu-id="0f66f-211">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-211">String</span></span> | <span data-ttu-id="0f66f-212">方向 hello 訊息流程、 接收或傳送。</span><span class="sxs-lookup"><span data-stu-id="0f66f-212">Direction of hello message flow, receive or send.</span></span> <span data-ttu-id="0f66f-213">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-213">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-214">messageId</span><span class="sxs-lookup"><span data-stu-id="0f66f-214">messageId</span></span> | <span data-ttu-id="0f66f-215">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-215">String</span></span> | <span data-ttu-id="0f66f-216">AS2 訊息識別碼。</span><span class="sxs-lookup"><span data-stu-id="0f66f-216">AS2 message ID.</span></span> <span data-ttu-id="0f66f-217">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-217">(Optional)</span></span> |
| <span data-ttu-id="0f66f-218">originalMessageId</span><span class="sxs-lookup"><span data-stu-id="0f66f-218">originalMessageId</span></span> |<span data-ttu-id="0f66f-219">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-219">String</span></span> | <span data-ttu-id="0f66f-220">AS2 原始訊息識別碼。</span><span class="sxs-lookup"><span data-stu-id="0f66f-220">AS2 original message ID.</span></span> <span data-ttu-id="0f66f-221">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-221">(Optional)</span></span> |
| <span data-ttu-id="0f66f-222">dispositionType</span><span class="sxs-lookup"><span data-stu-id="0f66f-222">dispositionType</span></span> | <span data-ttu-id="0f66f-223">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-223">String</span></span> | <span data-ttu-id="0f66f-224">MDN 處置類型值。</span><span class="sxs-lookup"><span data-stu-id="0f66f-224">MDN disposition type value.</span></span> <span data-ttu-id="0f66f-225">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-225">(Optional)</span></span> |
| <span data-ttu-id="0f66f-226">isMessageFailed</span><span class="sxs-lookup"><span data-stu-id="0f66f-226">isMessageFailed</span></span> |<span data-ttu-id="0f66f-227">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-227">Boolean</span></span> | <span data-ttu-id="0f66f-228">Hello AS2 訊息是否失敗。</span><span class="sxs-lookup"><span data-stu-id="0f66f-228">Whether hello AS2 message failed.</span></span> <span data-ttu-id="0f66f-229">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-229">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-230">isMessageSigned</span><span class="sxs-lookup"><span data-stu-id="0f66f-230">isMessageSigned</span></span> |<span data-ttu-id="0f66f-231">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-231">Boolean</span></span> | <span data-ttu-id="0f66f-232">Hello AS2 訊息是否簽署。</span><span class="sxs-lookup"><span data-stu-id="0f66f-232">Whether hello AS2 message was signed.</span></span> <span data-ttu-id="0f66f-233">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-233">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-234">isNrrEnabled</span><span class="sxs-lookup"><span data-stu-id="0f66f-234">isNrrEnabled</span></span> | <span data-ttu-id="0f66f-235">Boolean</span><span class="sxs-lookup"><span data-stu-id="0f66f-235">Boolean</span></span> | <span data-ttu-id="0f66f-236">如果不知道 hello 值，請使用預設值。</span><span class="sxs-lookup"><span data-stu-id="0f66f-236">Use default value if hello value is not known.</span></span> <span data-ttu-id="0f66f-237">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-237">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-238">StatusCode</span><span class="sxs-lookup"><span data-stu-id="0f66f-238">statusCode</span></span> | <span data-ttu-id="0f66f-239">例舉</span><span class="sxs-lookup"><span data-stu-id="0f66f-239">Enum</span></span> | <span data-ttu-id="0f66f-240">允許的值為 **Accepted**、**Rejected** 和 **AcceptedWithErrors**。</span><span class="sxs-lookup"><span data-stu-id="0f66f-240">Allowed values are **Accepted**, **Rejected**, and **AcceptedWithErrors**.</span></span> <span data-ttu-id="0f66f-241">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-241">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-242">micVerificationStatus</span><span class="sxs-lookup"><span data-stu-id="0f66f-242">micVerificationStatus</span></span> | <span data-ttu-id="0f66f-243">例舉</span><span class="sxs-lookup"><span data-stu-id="0f66f-243">Enum</span></span> | <span data-ttu-id="0f66f-244">允許的值為 **NotApplicable**、**Succeeded** 和 **Failed**。</span><span class="sxs-lookup"><span data-stu-id="0f66f-244">Allowed values are **NotApplicable**, **Succeeded**, and **Failed**.</span></span> <span data-ttu-id="0f66f-245">(必要)</span><span class="sxs-lookup"><span data-stu-id="0f66f-245">(Mandatory)</span></span> |
| <span data-ttu-id="0f66f-246">correlationMessageId</span><span class="sxs-lookup"><span data-stu-id="0f66f-246">correlationMessageId</span></span> | <span data-ttu-id="0f66f-247">String</span><span class="sxs-lookup"><span data-stu-id="0f66f-247">String</span></span> | <span data-ttu-id="0f66f-248">相互關連識別碼。</span><span class="sxs-lookup"><span data-stu-id="0f66f-248">Correlation ID.</span></span> <span data-ttu-id="0f66f-249">原始的 hello 依現狀識別碼 (hello 為設定 MDN 的 hello 訊息的訊息識別碼)。</span><span class="sxs-lookup"><span data-stu-id="0f66f-249">hello original messaged ID (hello message ID of hello message for which MDN is configured).</span></span> <span data-ttu-id="0f66f-250">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-250">(Optional)</span></span> |
| <span data-ttu-id="0f66f-251">incomingHeaders</span><span class="sxs-lookup"><span data-stu-id="0f66f-251">incomingHeaders</span></span> | <span data-ttu-id="0f66f-252">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="0f66f-252">Dictionary of JToken</span></span> | <span data-ttu-id="0f66f-253">指出內送訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f66f-253">Indicates incoming message header details.</span></span> <span data-ttu-id="0f66f-254">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-254">(Optional)</span></span> |
| <span data-ttu-id="0f66f-255">outgoingHeaders</span><span class="sxs-lookup"><span data-stu-id="0f66f-255">outgoingHeaders</span></span> |<span data-ttu-id="0f66f-256">JToken 的字典</span><span class="sxs-lookup"><span data-stu-id="0f66f-256">Dictionary of JToken</span></span> | <span data-ttu-id="0f66f-257">指出外寄訊息標頭詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0f66f-257">Indicates outgoing message header details.</span></span> <span data-ttu-id="0f66f-258">(選用)</span><span class="sxs-lookup"><span data-stu-id="0f66f-258">(Optional)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0f66f-259">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f66f-259">Next steps</span></span>
* <span data-ttu-id="0f66f-260">深入了解 hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0f66f-260">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>    
* <span data-ttu-id="0f66f-261">[深入了解監視 B2B 訊息](logic-apps-monitor-b2b-message.md)。</span><span class="sxs-lookup"><span data-stu-id="0f66f-261">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="0f66f-262">[深入了解 B2B 自訂追蹤結構描述](logic-apps-track-integration-account-custom-tracking-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="0f66f-262">Learn more about [B2B custom tracking schemas](logic-apps-track-integration-account-custom-tracking-schema.md).</span></span>   
* <span data-ttu-id="0f66f-263">深入了解 [X12 追蹤結構描述](logic-apps-track-integration-account-x12-tracking-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="0f66f-263">Learn more about [X12 tracking schemas](logic-apps-track-integration-account-x12-tracking-schema.md).</span></span>   
* <span data-ttu-id="0f66f-264">深入了解[追蹤 hello Operations Management Suite 入口網站中的 B2B 訊息](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)。</span><span class="sxs-lookup"><span data-stu-id="0f66f-264">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
