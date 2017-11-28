---
title: "Azure 服務匯流排要求-回應架構作業中的 AMQP 1.0 | Microsoft Docs"
description: "Microsoft Azure 服務匯流排要求/回應架構作業的清單。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: 756565b3da6e0a818d1ee3d5e17f942d96be14f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a><span data-ttu-id="117c2-103">Microsoft Azure 服務匯流排中的 AMQP 1.0：要求/回應架構作業</span><span class="sxs-lookup"><span data-stu-id="117c2-103">AMQP 1.0 in Microsoft Azure Service Bus: request-response-based operations</span></span>

<span data-ttu-id="117c2-104">本主題定義 Microsoft Azure 服務匯流排要求/回應架構作業的清單。</span><span class="sxs-lookup"><span data-stu-id="117c2-104">This topic defines the list of Microsoft Azure Service Bus request/response-based operations.</span></span> <span data-ttu-id="117c2-105">這項資訊是根據 AMQP 管理版本 1.0 工作草稿。</span><span class="sxs-lookup"><span data-stu-id="117c2-105">This information is based on the AMQP Management Version 1.0 working draft.</span></span>  
  
<span data-ttu-id="117c2-106">如需詳細的有線等級 AMQP 1.0 通訊協定指南，說明服務匯流排如何實作和建置 OASIS AMQP 技術規格，請參閱 [Azure 服務匯流排和事件中樞的 AMQP 1.0 通訊協定指南](service-bus-amqp-protocol-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="117c2-106">For a detailed wire-level AMQP 1.0 protocol guide, which explains how Service Bus implements and builds on the OASIS AMQP technical specification, see the [AMQP 1.0 in Azure Service Bus and Event Hubs protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="concepts"></a><span data-ttu-id="117c2-107">概念</span><span class="sxs-lookup"><span data-stu-id="117c2-107">Concepts</span></span>  
  
### <a name="entity-description"></a><span data-ttu-id="117c2-108">實體描述</span><span class="sxs-lookup"><span data-stu-id="117c2-108">Entity description</span></span>  

<span data-ttu-id="117c2-109">實體描述指是服務匯流排 [QueueDescription 類別](/dotnet/api/microsoft.servicebus.messaging.queuedescription)、[TopicDescription 類別](/dotnet/api/microsoft.servicebus.messaging.topicdescription)或 [SubscriptionDescription 類別](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription)物件。</span><span class="sxs-lookup"><span data-stu-id="117c2-109">An entity description refers to either a Service Bus [QueueDescription Class](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription Class](/dotnet/api/microsoft.servicebus.messaging.topicdescription), or [SubscriptionDescription Class](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) object.</span></span>  
  
### <a name="brokered-message"></a><span data-ttu-id="117c2-110">代理訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-110">Brokered message</span></span>  

<span data-ttu-id="117c2-111">代表服務匯流排中對應至 AMQP 訊息的訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-111">Represents a message in Service Bus, which is mapped to an AMQP message.</span></span> <span data-ttu-id="117c2-112">此對應會在[服務匯流排 AMQP 通訊協定指南](service-bus-amqp-protocol-guide.md)中定義。</span><span class="sxs-lookup"><span data-stu-id="117c2-112">The mapping is defined in the [Service Bus AMQP protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="attach-to-entity-management-node"></a><span data-ttu-id="117c2-113">附加至實體管理節點</span><span class="sxs-lookup"><span data-stu-id="117c2-113">Attach to entity management node</span></span>  

<span data-ttu-id="117c2-114">這份文件中所述的所有作業會遵循要求/回應模式、限定範圍至實體，並需要附加至實體管理節點。</span><span class="sxs-lookup"><span data-stu-id="117c2-114">All the operations described in this document follow a request/response pattern, are scoped to an entity, and require attaching to an entity management node.</span></span>  
  
### <a name="create-link-for-sending-requests"></a><span data-ttu-id="117c2-115">建立傳送要求的連結</span><span class="sxs-lookup"><span data-stu-id="117c2-115">Create link for sending requests</span></span>  

<span data-ttu-id="117c2-116">建立傳送要求的管理節點連結。</span><span class="sxs-lookup"><span data-stu-id="117c2-116">Creates a link to the management node for sending requests.</span></span>  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a><span data-ttu-id="117c2-117">建立接收回應的連結</span><span class="sxs-lookup"><span data-stu-id="117c2-117">Create link for receiving responses</span></span>  

<span data-ttu-id="117c2-118">建立連結，以便接收來自管理節點的回應。</span><span class="sxs-lookup"><span data-stu-id="117c2-118">Creates a link for receiving responses from the management node.</span></span>  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a><span data-ttu-id="117c2-119">傳輸要求訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-119">Transfer a request message</span></span>  

<span data-ttu-id="117c2-120">傳輸要求訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-120">Transfers a request message.</span></span>  
  
```  
requestLink.sendTransfer(  
        Message(  
                properties: {  
                        message-id: <request id>,  
                        reply-to: "<my response link unique address>"  
                },  
                application-properties: {  
                        "operation" -> "<operation>",  
                },  
        )  
```  
  
### <a name="receive-a-response-message"></a><span data-ttu-id="117c2-121">接收回應訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-121">Receive a response message</span></span>  

<span data-ttu-id="117c2-122">從回應連結接收回應訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-122">Receives the response message from the response link.</span></span>  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
<span data-ttu-id="117c2-123">回應訊息的格式如下：</span><span class="sxs-lookup"><span data-stu-id="117c2-123">The response message is in the following form:</span></span>
  
```  
Message(  
properties: {     
        correlation-id: <request id>  
    },  
    application-properties: {  
            "statusCode" -> <status code>,  
            "statusDescription" -> <status description>,  
           },         
)  
  
```  
  
### <a name="service-bus-entity-address"></a><span data-ttu-id="117c2-124">服務匯流排實體位址</span><span class="sxs-lookup"><span data-stu-id="117c2-124">Service Bus entity address</span></span>  

<span data-ttu-id="117c2-125">必須處理服務匯流排實體，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="117c2-125">Service Bus entities must be addressed as follows:</span></span>  
  
|<span data-ttu-id="117c2-126">實體類型</span><span class="sxs-lookup"><span data-stu-id="117c2-126">Entity type</span></span>|<span data-ttu-id="117c2-127">位址</span><span class="sxs-lookup"><span data-stu-id="117c2-127">Address</span></span>|<span data-ttu-id="117c2-128">範例</span><span class="sxs-lookup"><span data-stu-id="117c2-128">Example</span></span>|  
|-----------------|-------------|-------------|  
|<span data-ttu-id="117c2-129">佇列</span><span class="sxs-lookup"><span data-stu-id="117c2-129">queue</span></span>|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|<span data-ttu-id="117c2-130">主題</span><span class="sxs-lookup"><span data-stu-id="117c2-130">topic</span></span>|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|<span data-ttu-id="117c2-131">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="117c2-131">subscription</span></span>|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a><span data-ttu-id="117c2-132">訊息作業</span><span class="sxs-lookup"><span data-stu-id="117c2-132">Message operations</span></span>  
  
### <a name="message-renew-lock"></a><span data-ttu-id="117c2-133">訊息更新鎖定</span><span class="sxs-lookup"><span data-stu-id="117c2-133">Message Renew Lock</span></span>  

<span data-ttu-id="117c2-134">在實體描述中指定時擴充訊息的鎖定。</span><span class="sxs-lookup"><span data-stu-id="117c2-134">Extends the lock of a message by the time specified in the entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-135">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-135">Request</span></span>  

<span data-ttu-id="117c2-136">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-136">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-137">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-137">Key</span></span>|<span data-ttu-id="117c2-138">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-138">Value Type</span></span>|<span data-ttu-id="117c2-139">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-139">Required</span></span>|<span data-ttu-id="117c2-140">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-140">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-141">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-141">operation</span></span>|<span data-ttu-id="117c2-142">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-142">string</span></span>|<span data-ttu-id="117c2-143">是</span><span class="sxs-lookup"><span data-stu-id="117c2-143">Yes</span></span>|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-144">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-144">uint</span></span>|<span data-ttu-id="117c2-145">否</span><span class="sxs-lookup"><span data-stu-id="117c2-145">No</span></span>|<span data-ttu-id="117c2-146">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-146">Operation server timeout in milliseconds.</span></span>|  
  
 <span data-ttu-id="117c2-147">要求訊息本文必須由包含對應與下列項目的 amqp-value 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-147">The request message body must consist of an amqp-value section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-148">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-148">Key</span></span>|<span data-ttu-id="117c2-149">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-149">Value Type</span></span>|<span data-ttu-id="117c2-150">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-150">Required</span></span>|<span data-ttu-id="117c2-151">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-151">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|<span data-ttu-id="117c2-152">UUID 的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-152">array of uuid</span></span>|<span data-ttu-id="117c2-153">是</span><span class="sxs-lookup"><span data-stu-id="117c2-153">Yes</span></span>|<span data-ttu-id="117c2-154">要更新的訊息鎖定權杖。</span><span class="sxs-lookup"><span data-stu-id="117c2-154">Message lock tokens to renew.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-155">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-155">Response</span></span>  

<span data-ttu-id="117c2-156">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-156">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-157">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-157">Key</span></span>|<span data-ttu-id="117c2-158">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-158">Value Type</span></span>|<span data-ttu-id="117c2-159">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-159">Required</span></span>|<span data-ttu-id="117c2-160">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-160">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-161">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-161">statusCode</span></span>|<span data-ttu-id="117c2-162">int</span><span class="sxs-lookup"><span data-stu-id="117c2-162">int</span></span>|<span data-ttu-id="117c2-163">是</span><span class="sxs-lookup"><span data-stu-id="117c2-163">Yes</span></span>|<span data-ttu-id="117c2-164">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-164">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-165">200：確定 – 成功，否則失敗。</span><span class="sxs-lookup"><span data-stu-id="117c2-165">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="117c2-166">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-166">statusDescription</span></span>|<span data-ttu-id="117c2-167">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-167">string</span></span>|<span data-ttu-id="117c2-168">否</span><span class="sxs-lookup"><span data-stu-id="117c2-168">No</span></span>|<span data-ttu-id="117c2-169">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-169">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-170">回應訊息本文必須由包含對應與下列項目的 amqp-value 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-170">The response message body must consist of an amqp-value section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-171">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-171">Key</span></span>|<span data-ttu-id="117c2-172">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-172">Value Type</span></span>|<span data-ttu-id="117c2-173">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-173">Required</span></span>|<span data-ttu-id="117c2-174">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-174">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-175">到期日</span><span class="sxs-lookup"><span data-stu-id="117c2-175">expirations</span></span>|<span data-ttu-id="117c2-176">時間戳記的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-176">array of timestamp</span></span>|<span data-ttu-id="117c2-177">是</span><span class="sxs-lookup"><span data-stu-id="117c2-177">Yes</span></span>|<span data-ttu-id="117c2-178">對應到要求鎖定權杖的訊息鎖定權杖新期限。</span><span class="sxs-lookup"><span data-stu-id="117c2-178">Message lock token new expiration corresponding to the request lock tokens.</span></span>|  
  
### <a name="peek-message"></a><span data-ttu-id="117c2-179">查看訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-179">Peek Message</span></span>  

<span data-ttu-id="117c2-180">查看訊息而不用鎖定。</span><span class="sxs-lookup"><span data-stu-id="117c2-180">Peeks messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-181">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-181">Request</span></span>  

<span data-ttu-id="117c2-182">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-182">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-183">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-183">Key</span></span>|<span data-ttu-id="117c2-184">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-184">Value Type</span></span>|<span data-ttu-id="117c2-185">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-185">Required</span></span>|<span data-ttu-id="117c2-186">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-186">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-187">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-187">operation</span></span>|<span data-ttu-id="117c2-188">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-188">string</span></span>|<span data-ttu-id="117c2-189">是</span><span class="sxs-lookup"><span data-stu-id="117c2-189">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-190">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-190">uint</span></span>|<span data-ttu-id="117c2-191">否</span><span class="sxs-lookup"><span data-stu-id="117c2-191">No</span></span>|<span data-ttu-id="117c2-192">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-192">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-193">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-193">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-194">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-194">Key</span></span>|<span data-ttu-id="117c2-195">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-195">Value Type</span></span>|<span data-ttu-id="117c2-196">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-196">Required</span></span>|<span data-ttu-id="117c2-197">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-197">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|<span data-ttu-id="117c2-198">long</span><span class="sxs-lookup"><span data-stu-id="117c2-198">long</span></span>|<span data-ttu-id="117c2-199">是</span><span class="sxs-lookup"><span data-stu-id="117c2-199">Yes</span></span>|<span data-ttu-id="117c2-200">要開始查看的序號。</span><span class="sxs-lookup"><span data-stu-id="117c2-200">Sequence number from which to start peek.</span></span>|  
|`message-count`|<span data-ttu-id="117c2-201">int</span><span class="sxs-lookup"><span data-stu-id="117c2-201">int</span></span>|<span data-ttu-id="117c2-202">是</span><span class="sxs-lookup"><span data-stu-id="117c2-202">Yes</span></span>|<span data-ttu-id="117c2-203">要查看的訊息數目上限。</span><span class="sxs-lookup"><span data-stu-id="117c2-203">Maximum number of messages to peek.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-204">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-204">Response</span></span>  

<span data-ttu-id="117c2-205">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-205">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-206">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-206">Key</span></span>|<span data-ttu-id="117c2-207">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-207">Value Type</span></span>|<span data-ttu-id="117c2-208">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-208">Required</span></span>|<span data-ttu-id="117c2-209">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-209">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-210">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-210">statusCode</span></span>|<span data-ttu-id="117c2-211">int</span><span class="sxs-lookup"><span data-stu-id="117c2-211">int</span></span>|<span data-ttu-id="117c2-212">是</span><span class="sxs-lookup"><span data-stu-id="117c2-212">Yes</span></span>|<span data-ttu-id="117c2-213">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-213">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-214">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-214">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="117c2-215">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-215">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="117c2-216">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-216">statusDescription</span></span>|<span data-ttu-id="117c2-217">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-217">string</span></span>|<span data-ttu-id="117c2-218">否</span><span class="sxs-lookup"><span data-stu-id="117c2-218">No</span></span>|<span data-ttu-id="117c2-219">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-219">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-220">回應訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-220">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-221">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-221">Key</span></span>|<span data-ttu-id="117c2-222">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-222">Value Type</span></span>|<span data-ttu-id="117c2-223">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-223">Required</span></span>|<span data-ttu-id="117c2-224">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-224">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-225">上限</span><span class="sxs-lookup"><span data-stu-id="117c2-225">messages</span></span>|<span data-ttu-id="117c2-226">對應的清單</span><span class="sxs-lookup"><span data-stu-id="117c2-226">list of maps</span></span>|<span data-ttu-id="117c2-227">是</span><span class="sxs-lookup"><span data-stu-id="117c2-227">Yes</span></span>|<span data-ttu-id="117c2-228">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="117c2-228">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="117c2-229">代表訊息的對應必須包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="117c2-229">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="117c2-230">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-230">Key</span></span>|<span data-ttu-id="117c2-231">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-231">Value Type</span></span>|<span data-ttu-id="117c2-232">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-232">Required</span></span>|<span data-ttu-id="117c2-233">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-233">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-234">訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-234">message</span></span>|<span data-ttu-id="117c2-235">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-235">array of byte</span></span>|<span data-ttu-id="117c2-236">是</span><span class="sxs-lookup"><span data-stu-id="117c2-236">Yes</span></span>|<span data-ttu-id="117c2-237">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-237">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="schedule-message"></a><span data-ttu-id="117c2-238">排程訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-238">Schedule Message</span></span>  

<span data-ttu-id="117c2-239">排程訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-239">Schedules messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-240">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-240">Request</span></span>  

<span data-ttu-id="117c2-241">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-241">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-242">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-242">Key</span></span>|<span data-ttu-id="117c2-243">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-243">Value Type</span></span>|<span data-ttu-id="117c2-244">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-244">Required</span></span>|<span data-ttu-id="117c2-245">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-245">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-246">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-246">operation</span></span>|<span data-ttu-id="117c2-247">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-247">string</span></span>|<span data-ttu-id="117c2-248">是</span><span class="sxs-lookup"><span data-stu-id="117c2-248">Yes</span></span>|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-249">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-249">uint</span></span>|<span data-ttu-id="117c2-250">否</span><span class="sxs-lookup"><span data-stu-id="117c2-250">No</span></span>|<span data-ttu-id="117c2-251">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-251">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-252">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-252">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-253">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-253">Key</span></span>|<span data-ttu-id="117c2-254">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-254">Value Type</span></span>|<span data-ttu-id="117c2-255">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-255">Required</span></span>|<span data-ttu-id="117c2-256">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-256">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-257">上限</span><span class="sxs-lookup"><span data-stu-id="117c2-257">messages</span></span>|<span data-ttu-id="117c2-258">對應的清單</span><span class="sxs-lookup"><span data-stu-id="117c2-258">list of maps</span></span>|<span data-ttu-id="117c2-259">是</span><span class="sxs-lookup"><span data-stu-id="117c2-259">Yes</span></span>|<span data-ttu-id="117c2-260">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="117c2-260">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="117c2-261">代表訊息的對應必須包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="117c2-261">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="117c2-262">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-262">Key</span></span>|<span data-ttu-id="117c2-263">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-263">Value Type</span></span>|<span data-ttu-id="117c2-264">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-264">Required</span></span>|<span data-ttu-id="117c2-265">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-265">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-266">message-id</span><span class="sxs-lookup"><span data-stu-id="117c2-266">message-id</span></span>|<span data-ttu-id="117c2-267">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-267">string</span></span>|<span data-ttu-id="117c2-268">是</span><span class="sxs-lookup"><span data-stu-id="117c2-268">Yes</span></span>|<span data-ttu-id="117c2-269">`amqpMessage.Properties.MessageId` 為字串</span><span class="sxs-lookup"><span data-stu-id="117c2-269">`amqpMessage.Properties.MessageId` as string</span></span>|  
|<span data-ttu-id="117c2-270">session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-270">session-id</span></span>|<span data-ttu-id="117c2-271">string</span><span class="sxs-lookup"><span data-stu-id="117c2-271">string</span></span>|<span data-ttu-id="117c2-272">是</span><span class="sxs-lookup"><span data-stu-id="117c2-272">Yes</span></span>|`amqpMessage.Properties.GroupId as string`|  
|<span data-ttu-id="117c2-273">partition-key</span><span class="sxs-lookup"><span data-stu-id="117c2-273">partition-key</span></span>|<span data-ttu-id="117c2-274">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-274">string</span></span>|<span data-ttu-id="117c2-275">是</span><span class="sxs-lookup"><span data-stu-id="117c2-275">Yes</span></span>|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|<span data-ttu-id="117c2-276">訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-276">message</span></span>|<span data-ttu-id="117c2-277">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-277">array of byte</span></span>|<span data-ttu-id="117c2-278">是</span><span class="sxs-lookup"><span data-stu-id="117c2-278">Yes</span></span>|<span data-ttu-id="117c2-279">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-279">AMQP 1.0 wire-encoded message.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-280">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-280">Response</span></span>  

<span data-ttu-id="117c2-281">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-281">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-282">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-282">Key</span></span>|<span data-ttu-id="117c2-283">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-283">Value Type</span></span>|<span data-ttu-id="117c2-284">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-284">Required</span></span>|<span data-ttu-id="117c2-285">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-285">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-286">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-286">statusCode</span></span>|<span data-ttu-id="117c2-287">int</span><span class="sxs-lookup"><span data-stu-id="117c2-287">int</span></span>|<span data-ttu-id="117c2-288">是</span><span class="sxs-lookup"><span data-stu-id="117c2-288">Yes</span></span>|<span data-ttu-id="117c2-289">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-289">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-290">200：確定 – 成功，否則失敗。</span><span class="sxs-lookup"><span data-stu-id="117c2-290">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="117c2-291">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-291">statusDescription</span></span>|<span data-ttu-id="117c2-292">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-292">string</span></span>|<span data-ttu-id="117c2-293">否</span><span class="sxs-lookup"><span data-stu-id="117c2-293">No</span></span>|<span data-ttu-id="117c2-294">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-294">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-295">回應訊息本文必須由包含對應與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-295">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-296">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-296">Key</span></span>|<span data-ttu-id="117c2-297">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-297">Value Type</span></span>|<span data-ttu-id="117c2-298">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-298">Required</span></span>|<span data-ttu-id="117c2-299">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-299">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-300">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="117c2-300">sequence-numbers</span></span>|<span data-ttu-id="117c2-301">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-301">array of long</span></span>|<span data-ttu-id="117c2-302">是</span><span class="sxs-lookup"><span data-stu-id="117c2-302">Yes</span></span>|<span data-ttu-id="117c2-303">排定訊息的序號。</span><span class="sxs-lookup"><span data-stu-id="117c2-303">Sequence number of scheduled messages.</span></span> <span data-ttu-id="117c2-304">序號用來取消。</span><span class="sxs-lookup"><span data-stu-id="117c2-304">Sequence number is used to cancel.</span></span>|  
  
### <a name="cancel-scheduled-message"></a><span data-ttu-id="117c2-305">取消排定的訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-305">Cancel Scheduled Message</span></span>  

<span data-ttu-id="117c2-306">取消排定的訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-306">Cancels scheduled messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-307">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-307">Request</span></span>  

<span data-ttu-id="117c2-308">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-308">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-309">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-309">Key</span></span>|<span data-ttu-id="117c2-310">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-310">Value Type</span></span>|<span data-ttu-id="117c2-311">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-311">Required</span></span>|<span data-ttu-id="117c2-312">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-312">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-313">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-313">operation</span></span>|<span data-ttu-id="117c2-314">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-314">string</span></span>|<span data-ttu-id="117c2-315">是</span><span class="sxs-lookup"><span data-stu-id="117c2-315">Yes</span></span>|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-316">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-316">uint</span></span>|<span data-ttu-id="117c2-317">否</span><span class="sxs-lookup"><span data-stu-id="117c2-317">No</span></span>|<span data-ttu-id="117c2-318">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-318">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-319">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-319">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-320">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-320">Key</span></span>|<span data-ttu-id="117c2-321">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-321">Value Type</span></span>|<span data-ttu-id="117c2-322">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-322">Required</span></span>|<span data-ttu-id="117c2-323">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-323">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-324">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="117c2-324">sequence-numbers</span></span>|<span data-ttu-id="117c2-325">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-325">array of long</span></span>|<span data-ttu-id="117c2-326">是</span><span class="sxs-lookup"><span data-stu-id="117c2-326">Yes</span></span>|<span data-ttu-id="117c2-327">要取消之排程訊息的序號。</span><span class="sxs-lookup"><span data-stu-id="117c2-327">Sequence numbers of scheduled messages to cancel.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-328">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-328">Response</span></span>  

<span data-ttu-id="117c2-329">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-329">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-330">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-330">Key</span></span>|<span data-ttu-id="117c2-331">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-331">Value Type</span></span>|<span data-ttu-id="117c2-332">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-332">Required</span></span>|<span data-ttu-id="117c2-333">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-333">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-334">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-334">statusCode</span></span>|<span data-ttu-id="117c2-335">int</span><span class="sxs-lookup"><span data-stu-id="117c2-335">int</span></span>|<span data-ttu-id="117c2-336">是</span><span class="sxs-lookup"><span data-stu-id="117c2-336">Yes</span></span>|<span data-ttu-id="117c2-337">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-337">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-338">200：確定 – 成功，否則失敗。</span><span class="sxs-lookup"><span data-stu-id="117c2-338">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="117c2-339">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-339">statusDescription</span></span>|<span data-ttu-id="117c2-340">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-340">string</span></span>|<span data-ttu-id="117c2-341">否</span><span class="sxs-lookup"><span data-stu-id="117c2-341">No</span></span>|<span data-ttu-id="117c2-342">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-342">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-343">回應訊息本文必須由包含對應與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-343">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-344">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-344">Key</span></span>|<span data-ttu-id="117c2-345">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-345">Value Type</span></span>|<span data-ttu-id="117c2-346">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-346">Required</span></span>|<span data-ttu-id="117c2-347">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-347">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-348">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="117c2-348">sequence-numbers</span></span>|<span data-ttu-id="117c2-349">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-349">array of long</span></span>|<span data-ttu-id="117c2-350">是</span><span class="sxs-lookup"><span data-stu-id="117c2-350">Yes</span></span>|<span data-ttu-id="117c2-351">排定訊息的序號。</span><span class="sxs-lookup"><span data-stu-id="117c2-351">Sequence number of scheduled messages.</span></span> <span data-ttu-id="117c2-352">序號用來取消。</span><span class="sxs-lookup"><span data-stu-id="117c2-352">Sequence number is used to cancel.</span></span>|  
  
## <a name="session-operations"></a><span data-ttu-id="117c2-353">工作階段作業</span><span class="sxs-lookup"><span data-stu-id="117c2-353">Session Operations</span></span>  
  
### <a name="session-renew-lock"></a><span data-ttu-id="117c2-354">工作階段更新鎖定</span><span class="sxs-lookup"><span data-stu-id="117c2-354">Session Renew Lock</span></span>  

<span data-ttu-id="117c2-355">在實體描述中指定時擴充訊息的鎖定。</span><span class="sxs-lookup"><span data-stu-id="117c2-355">Extends the lock of a message by the time specified in the entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-356">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-356">Request</span></span>  

<span data-ttu-id="117c2-357">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-357">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-358">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-358">Key</span></span>|<span data-ttu-id="117c2-359">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-359">Value Type</span></span>|<span data-ttu-id="117c2-360">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-360">Required</span></span>|<span data-ttu-id="117c2-361">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-361">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-362">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-362">operation</span></span>|<span data-ttu-id="117c2-363">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-363">string</span></span>|<span data-ttu-id="117c2-364">是</span><span class="sxs-lookup"><span data-stu-id="117c2-364">Yes</span></span>|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-365">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-365">uint</span></span>|<span data-ttu-id="117c2-366">否</span><span class="sxs-lookup"><span data-stu-id="117c2-366">No</span></span>|<span data-ttu-id="117c2-367">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-367">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-368">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-368">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-369">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-369">Key</span></span>|<span data-ttu-id="117c2-370">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-370">Value Type</span></span>|<span data-ttu-id="117c2-371">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-371">Required</span></span>|<span data-ttu-id="117c2-372">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-372">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-373">session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-373">session-id</span></span>|<span data-ttu-id="117c2-374">string</span><span class="sxs-lookup"><span data-stu-id="117c2-374">string</span></span>|<span data-ttu-id="117c2-375">是</span><span class="sxs-lookup"><span data-stu-id="117c2-375">Yes</span></span>|<span data-ttu-id="117c2-376">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="117c2-376">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-377">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-377">Response</span></span>  

<span data-ttu-id="117c2-378">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-378">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-379">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-379">Key</span></span>|<span data-ttu-id="117c2-380">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-380">Value Type</span></span>|<span data-ttu-id="117c2-381">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-381">Required</span></span>|<span data-ttu-id="117c2-382">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-382">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-383">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-383">statusCode</span></span>|<span data-ttu-id="117c2-384">int</span><span class="sxs-lookup"><span data-stu-id="117c2-384">int</span></span>|<span data-ttu-id="117c2-385">是</span><span class="sxs-lookup"><span data-stu-id="117c2-385">Yes</span></span>|<span data-ttu-id="117c2-386">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-386">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-387">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-387">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="117c2-388">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-388">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="117c2-389">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-389">statusDescription</span></span>|<span data-ttu-id="117c2-390">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-390">string</span></span>|<span data-ttu-id="117c2-391">否</span><span class="sxs-lookup"><span data-stu-id="117c2-391">No</span></span>|<span data-ttu-id="117c2-392">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-392">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-393">回應訊息本文必須由包含對應與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-393">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-394">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-394">Key</span></span>|<span data-ttu-id="117c2-395">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-395">Value Type</span></span>|<span data-ttu-id="117c2-396">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-396">Required</span></span>|<span data-ttu-id="117c2-397">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-397">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-398">expiration</span><span class="sxs-lookup"><span data-stu-id="117c2-398">expiration</span></span>|<span data-ttu-id="117c2-399">timestamp</span><span class="sxs-lookup"><span data-stu-id="117c2-399">timestamp</span></span>|<span data-ttu-id="117c2-400">是</span><span class="sxs-lookup"><span data-stu-id="117c2-400">Yes</span></span>|<span data-ttu-id="117c2-401">新的到期日。</span><span class="sxs-lookup"><span data-stu-id="117c2-401">New expiration.</span></span>|  
  
### <a name="peek-session-message"></a><span data-ttu-id="117c2-402">查看工作階段訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-402">Peek Session Message</span></span>  

<span data-ttu-id="117c2-403">查看工作階段訊息而不用鎖定。</span><span class="sxs-lookup"><span data-stu-id="117c2-403">Peeks session messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-404">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-404">Request</span></span>  

<span data-ttu-id="117c2-405">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-405">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-406">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-406">Key</span></span>|<span data-ttu-id="117c2-407">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-407">Value Type</span></span>|<span data-ttu-id="117c2-408">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-408">Required</span></span>|<span data-ttu-id="117c2-409">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-409">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-410">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-410">operation</span></span>|<span data-ttu-id="117c2-411">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-411">string</span></span>|<span data-ttu-id="117c2-412">是</span><span class="sxs-lookup"><span data-stu-id="117c2-412">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-413">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-413">uint</span></span>|<span data-ttu-id="117c2-414">否</span><span class="sxs-lookup"><span data-stu-id="117c2-414">No</span></span>|<span data-ttu-id="117c2-415">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-415">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-416">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-416">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-417">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-417">Key</span></span>|<span data-ttu-id="117c2-418">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-418">Value Type</span></span>|<span data-ttu-id="117c2-419">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-419">Required</span></span>|<span data-ttu-id="117c2-420">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-420">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-421">from-sequence-number</span><span class="sxs-lookup"><span data-stu-id="117c2-421">from-sequence-number</span></span>|<span data-ttu-id="117c2-422">long</span><span class="sxs-lookup"><span data-stu-id="117c2-422">long</span></span>|<span data-ttu-id="117c2-423">是</span><span class="sxs-lookup"><span data-stu-id="117c2-423">Yes</span></span>|<span data-ttu-id="117c2-424">要開始查看的序號。</span><span class="sxs-lookup"><span data-stu-id="117c2-424">Sequence number from which to start peek.</span></span>|  
|<span data-ttu-id="117c2-425">message-count</span><span class="sxs-lookup"><span data-stu-id="117c2-425">message-count</span></span>|<span data-ttu-id="117c2-426">int</span><span class="sxs-lookup"><span data-stu-id="117c2-426">int</span></span>|<span data-ttu-id="117c2-427">是</span><span class="sxs-lookup"><span data-stu-id="117c2-427">Yes</span></span>|<span data-ttu-id="117c2-428">要查看的訊息數目上限。</span><span class="sxs-lookup"><span data-stu-id="117c2-428">Maximum number of messages to peek.</span></span>|  
|<span data-ttu-id="117c2-429">session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-429">session-id</span></span>|<span data-ttu-id="117c2-430">string</span><span class="sxs-lookup"><span data-stu-id="117c2-430">string</span></span>|<span data-ttu-id="117c2-431">是</span><span class="sxs-lookup"><span data-stu-id="117c2-431">Yes</span></span>|<span data-ttu-id="117c2-432">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="117c2-432">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-433">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-433">Response</span></span>  

<span data-ttu-id="117c2-434">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-434">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-435">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-435">Key</span></span>|<span data-ttu-id="117c2-436">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-436">Value Type</span></span>|<span data-ttu-id="117c2-437">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-437">Required</span></span>|<span data-ttu-id="117c2-438">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-438">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-439">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-439">statusCode</span></span>|<span data-ttu-id="117c2-440">int</span><span class="sxs-lookup"><span data-stu-id="117c2-440">int</span></span>|<span data-ttu-id="117c2-441">是</span><span class="sxs-lookup"><span data-stu-id="117c2-441">Yes</span></span>|<span data-ttu-id="117c2-442">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-442">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-443">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-443">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="117c2-444">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-444">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="117c2-445">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-445">statusDescription</span></span>|<span data-ttu-id="117c2-446">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-446">string</span></span>|<span data-ttu-id="117c2-447">否</span><span class="sxs-lookup"><span data-stu-id="117c2-447">No</span></span>|<span data-ttu-id="117c2-448">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-448">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-449">回應訊息本文必須由包含對應與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-449">The response message body must consist of an **amqp-value** section containing a map with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-450">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-450">Key</span></span>|<span data-ttu-id="117c2-451">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-451">Value Type</span></span>|<span data-ttu-id="117c2-452">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-452">Required</span></span>|<span data-ttu-id="117c2-453">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-453">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-454">上限</span><span class="sxs-lookup"><span data-stu-id="117c2-454">messages</span></span>|<span data-ttu-id="117c2-455">對應的清單</span><span class="sxs-lookup"><span data-stu-id="117c2-455">list of maps</span></span>|<span data-ttu-id="117c2-456">是</span><span class="sxs-lookup"><span data-stu-id="117c2-456">Yes</span></span>|<span data-ttu-id="117c2-457">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="117c2-457">List of messages in which every map represents a message.</span></span>|  
  
 <span data-ttu-id="117c2-458">代表訊息的對應必須包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="117c2-458">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="117c2-459">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-459">Key</span></span>|<span data-ttu-id="117c2-460">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-460">Value Type</span></span>|<span data-ttu-id="117c2-461">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-461">Required</span></span>|<span data-ttu-id="117c2-462">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-462">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-463">訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-463">message</span></span>|<span data-ttu-id="117c2-464">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-464">array of byte</span></span>|<span data-ttu-id="117c2-465">是</span><span class="sxs-lookup"><span data-stu-id="117c2-465">Yes</span></span>|<span data-ttu-id="117c2-466">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-466">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="set-session-state"></a><span data-ttu-id="117c2-467">設定工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="117c2-467">Set Session State</span></span>  

<span data-ttu-id="117c2-468">設定工作階段的狀態。</span><span class="sxs-lookup"><span data-stu-id="117c2-468">Sets the state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-469">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-469">Request</span></span>  

<span data-ttu-id="117c2-470">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-470">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-471">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-471">Key</span></span>|<span data-ttu-id="117c2-472">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-472">Value Type</span></span>|<span data-ttu-id="117c2-473">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-473">Required</span></span>|<span data-ttu-id="117c2-474">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-474">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-475">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-475">operation</span></span>|<span data-ttu-id="117c2-476">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-476">string</span></span>|<span data-ttu-id="117c2-477">是</span><span class="sxs-lookup"><span data-stu-id="117c2-477">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-478">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-478">uint</span></span>|<span data-ttu-id="117c2-479">否</span><span class="sxs-lookup"><span data-stu-id="117c2-479">No</span></span>|<span data-ttu-id="117c2-480">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-480">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-481">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-481">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-482">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-482">Key</span></span>|<span data-ttu-id="117c2-483">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-483">Value Type</span></span>|<span data-ttu-id="117c2-484">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-484">Required</span></span>|<span data-ttu-id="117c2-485">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-485">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-486">session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-486">session-id</span></span>|<span data-ttu-id="117c2-487">string</span><span class="sxs-lookup"><span data-stu-id="117c2-487">string</span></span>|<span data-ttu-id="117c2-488">是</span><span class="sxs-lookup"><span data-stu-id="117c2-488">Yes</span></span>|<span data-ttu-id="117c2-489">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="117c2-489">Session ID.</span></span>|  
|<span data-ttu-id="117c2-490">session-state</span><span class="sxs-lookup"><span data-stu-id="117c2-490">session-state</span></span>|<span data-ttu-id="117c2-491">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-491">array of bytes</span></span>|<span data-ttu-id="117c2-492">是</span><span class="sxs-lookup"><span data-stu-id="117c2-492">Yes</span></span>|<span data-ttu-id="117c2-493">不透明的二進位資料。</span><span class="sxs-lookup"><span data-stu-id="117c2-493">Opaque binary data.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-494">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-494">Response</span></span>  

<span data-ttu-id="117c2-495">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-495">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-496">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-496">Key</span></span>|<span data-ttu-id="117c2-497">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-497">Value Type</span></span>|<span data-ttu-id="117c2-498">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-498">Required</span></span>|<span data-ttu-id="117c2-499">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-499">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-500">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-500">statusCode</span></span>|<span data-ttu-id="117c2-501">int</span><span class="sxs-lookup"><span data-stu-id="117c2-501">int</span></span>|<span data-ttu-id="117c2-502">是</span><span class="sxs-lookup"><span data-stu-id="117c2-502">Yes</span></span>|<span data-ttu-id="117c2-503">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-503">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-504">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="117c2-504">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="117c2-505">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-505">statusDescription</span></span>|<span data-ttu-id="117c2-506">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-506">string</span></span>|<span data-ttu-id="117c2-507">否</span><span class="sxs-lookup"><span data-stu-id="117c2-507">No</span></span>|<span data-ttu-id="117c2-508">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-508">Description of the status.</span></span>|  
  
### <a name="get-session-state"></a><span data-ttu-id="117c2-509">取得工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="117c2-509">Get Session State</span></span>  

<span data-ttu-id="117c2-510">取得工作階段的狀態。</span><span class="sxs-lookup"><span data-stu-id="117c2-510">Gets the state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-511">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-511">Request</span></span>  

<span data-ttu-id="117c2-512">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-512">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-513">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-513">Key</span></span>|<span data-ttu-id="117c2-514">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-514">Value Type</span></span>|<span data-ttu-id="117c2-515">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-515">Required</span></span>|<span data-ttu-id="117c2-516">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-516">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-517">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-517">operation</span></span>|<span data-ttu-id="117c2-518">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-518">string</span></span>|<span data-ttu-id="117c2-519">是</span><span class="sxs-lookup"><span data-stu-id="117c2-519">Yes</span></span>|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-520">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-520">uint</span></span>|<span data-ttu-id="117c2-521">否</span><span class="sxs-lookup"><span data-stu-id="117c2-521">No</span></span>|<span data-ttu-id="117c2-522">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-522">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-523">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-523">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-524">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-524">Key</span></span>|<span data-ttu-id="117c2-525">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-525">Value Type</span></span>|<span data-ttu-id="117c2-526">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-526">Required</span></span>|<span data-ttu-id="117c2-527">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-527">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-528">session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-528">session-id</span></span>|<span data-ttu-id="117c2-529">string</span><span class="sxs-lookup"><span data-stu-id="117c2-529">string</span></span>|<span data-ttu-id="117c2-530">是</span><span class="sxs-lookup"><span data-stu-id="117c2-530">Yes</span></span>|<span data-ttu-id="117c2-531">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="117c2-531">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-532">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-532">Response</span></span>  

<span data-ttu-id="117c2-533">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-533">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-534">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-534">Key</span></span>|<span data-ttu-id="117c2-535">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-535">Value Type</span></span>|<span data-ttu-id="117c2-536">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-536">Required</span></span>|<span data-ttu-id="117c2-537">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-537">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-538">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-538">statusCode</span></span>|<span data-ttu-id="117c2-539">int</span><span class="sxs-lookup"><span data-stu-id="117c2-539">int</span></span>|<span data-ttu-id="117c2-540">是</span><span class="sxs-lookup"><span data-stu-id="117c2-540">Yes</span></span>|<span data-ttu-id="117c2-541">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-541">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-542">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="117c2-542">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="117c2-543">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-543">statusDescription</span></span>|<span data-ttu-id="117c2-544">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-544">string</span></span>|<span data-ttu-id="117c2-545">否</span><span class="sxs-lookup"><span data-stu-id="117c2-545">No</span></span>|<span data-ttu-id="117c2-546">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-546">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-547">回應訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-547">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-548">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-548">Key</span></span>|<span data-ttu-id="117c2-549">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-549">Value Type</span></span>|<span data-ttu-id="117c2-550">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-550">Required</span></span>|<span data-ttu-id="117c2-551">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-551">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-552">session-state</span><span class="sxs-lookup"><span data-stu-id="117c2-552">session-state</span></span>|<span data-ttu-id="117c2-553">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-553">array of bytes</span></span>|<span data-ttu-id="117c2-554">是</span><span class="sxs-lookup"><span data-stu-id="117c2-554">Yes</span></span>|<span data-ttu-id="117c2-555">不透明的二進位資料。</span><span class="sxs-lookup"><span data-stu-id="117c2-555">Opaque binary data.</span></span>|  
  
### <a name="enumerate-sessions"></a><span data-ttu-id="117c2-556">列舉工作階段</span><span class="sxs-lookup"><span data-stu-id="117c2-556">Enumerate Sessions</span></span>  

<span data-ttu-id="117c2-557">列舉訊息實體上的工作階段。</span><span class="sxs-lookup"><span data-stu-id="117c2-557">Enumerates sessions on a messaging entity.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-558">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-558">Request</span></span>  

<span data-ttu-id="117c2-559">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-559">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-560">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-560">Key</span></span>|<span data-ttu-id="117c2-561">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-561">Value Type</span></span>|<span data-ttu-id="117c2-562">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-562">Required</span></span>|<span data-ttu-id="117c2-563">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-563">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-564">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-564">operation</span></span>|<span data-ttu-id="117c2-565">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-565">string</span></span>|<span data-ttu-id="117c2-566">是</span><span class="sxs-lookup"><span data-stu-id="117c2-566">Yes</span></span>|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-567">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-567">uint</span></span>|<span data-ttu-id="117c2-568">否</span><span class="sxs-lookup"><span data-stu-id="117c2-568">No</span></span>|<span data-ttu-id="117c2-569">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-569">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-570">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-570">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-571">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-571">Key</span></span>|<span data-ttu-id="117c2-572">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-572">Value Type</span></span>|<span data-ttu-id="117c2-573">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-573">Required</span></span>|<span data-ttu-id="117c2-574">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-574">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-575">last-updated-time</span><span class="sxs-lookup"><span data-stu-id="117c2-575">last-updated-time</span></span>|<span data-ttu-id="117c2-576">timestamp</span><span class="sxs-lookup"><span data-stu-id="117c2-576">timestamp</span></span>|<span data-ttu-id="117c2-577">是</span><span class="sxs-lookup"><span data-stu-id="117c2-577">Yes</span></span>|<span data-ttu-id="117c2-578">篩選以在指定時間之後只包括更新的工作階段。</span><span class="sxs-lookup"><span data-stu-id="117c2-578">Filter to include only sessions updated after a given time.</span></span>|  
|<span data-ttu-id="117c2-579">skip</span><span class="sxs-lookup"><span data-stu-id="117c2-579">skip</span></span>|<span data-ttu-id="117c2-580">int</span><span class="sxs-lookup"><span data-stu-id="117c2-580">int</span></span>|<span data-ttu-id="117c2-581">是</span><span class="sxs-lookup"><span data-stu-id="117c2-581">Yes</span></span>|<span data-ttu-id="117c2-582">略過工作階段數。</span><span class="sxs-lookup"><span data-stu-id="117c2-582">Skip a number of sessions.</span></span>|  
|<span data-ttu-id="117c2-583">top</span><span class="sxs-lookup"><span data-stu-id="117c2-583">top</span></span>|<span data-ttu-id="117c2-584">int</span><span class="sxs-lookup"><span data-stu-id="117c2-584">int</span></span>|<span data-ttu-id="117c2-585">是</span><span class="sxs-lookup"><span data-stu-id="117c2-585">Yes</span></span>|<span data-ttu-id="117c2-586">工作階段數上限。</span><span class="sxs-lookup"><span data-stu-id="117c2-586">Maximum number of sessions.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-587">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-587">Response</span></span>  

<span data-ttu-id="117c2-588">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-588">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-589">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-589">Key</span></span>|<span data-ttu-id="117c2-590">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-590">Value Type</span></span>|<span data-ttu-id="117c2-591">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-591">Required</span></span>|<span data-ttu-id="117c2-592">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-592">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-593">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-593">statusCode</span></span>|<span data-ttu-id="117c2-594">int</span><span class="sxs-lookup"><span data-stu-id="117c2-594">int</span></span>|<span data-ttu-id="117c2-595">是</span><span class="sxs-lookup"><span data-stu-id="117c2-595">Yes</span></span>|<span data-ttu-id="117c2-596">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-596">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-597">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-597">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="117c2-598">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-598">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="117c2-599">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-599">statusDescription</span></span>|<span data-ttu-id="117c2-600">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-600">string</span></span>|<span data-ttu-id="117c2-601">否</span><span class="sxs-lookup"><span data-stu-id="117c2-601">No</span></span>|<span data-ttu-id="117c2-602">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-602">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-603">回應訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-603">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-604">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-604">Key</span></span>|<span data-ttu-id="117c2-605">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-605">Value Type</span></span>|<span data-ttu-id="117c2-606">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-606">Required</span></span>|<span data-ttu-id="117c2-607">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-607">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-608">skip</span><span class="sxs-lookup"><span data-stu-id="117c2-608">skip</span></span>|<span data-ttu-id="117c2-609">int</span><span class="sxs-lookup"><span data-stu-id="117c2-609">int</span></span>|<span data-ttu-id="117c2-610">是</span><span class="sxs-lookup"><span data-stu-id="117c2-610">Yes</span></span>|<span data-ttu-id="117c2-611">如果狀態碼為 200 所略過的工作階段數。</span><span class="sxs-lookup"><span data-stu-id="117c2-611">Number of skipped sessions if status code is 200.</span></span>|  
|<span data-ttu-id="117c2-612">sessions-ids</span><span class="sxs-lookup"><span data-stu-id="117c2-612">sessions-ids</span></span>|<span data-ttu-id="117c2-613">字串的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-613">array of strings</span></span>|<span data-ttu-id="117c2-614">是</span><span class="sxs-lookup"><span data-stu-id="117c2-614">Yes</span></span>|<span data-ttu-id="117c2-615">如果狀態碼為 200 的工作階段識別碼陣列。</span><span class="sxs-lookup"><span data-stu-id="117c2-615">Array of session IDs if status code is 200.</span></span>|  
  
## <a name="rule-operations"></a><span data-ttu-id="117c2-616">規則作業</span><span class="sxs-lookup"><span data-stu-id="117c2-616">Rule operations</span></span>  
  
### <a name="add-rule"></a><span data-ttu-id="117c2-617">新增規則</span><span class="sxs-lookup"><span data-stu-id="117c2-617">Add Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-618">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-618">Request</span></span>  

<span data-ttu-id="117c2-619">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-619">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-620">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-620">Key</span></span>|<span data-ttu-id="117c2-621">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-621">Value Type</span></span>|<span data-ttu-id="117c2-622">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-622">Required</span></span>|<span data-ttu-id="117c2-623">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-623">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-624">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-624">operation</span></span>|<span data-ttu-id="117c2-625">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-625">string</span></span>|<span data-ttu-id="117c2-626">是</span><span class="sxs-lookup"><span data-stu-id="117c2-626">Yes</span></span>|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-627">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-627">uint</span></span>|<span data-ttu-id="117c2-628">否</span><span class="sxs-lookup"><span data-stu-id="117c2-628">No</span></span>|<span data-ttu-id="117c2-629">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-629">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-630">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-630">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-631">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-631">Key</span></span>|<span data-ttu-id="117c2-632">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-632">Value Type</span></span>|<span data-ttu-id="117c2-633">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-633">Required</span></span>|<span data-ttu-id="117c2-634">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-634">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-635">rule-name</span><span class="sxs-lookup"><span data-stu-id="117c2-635">rule-name</span></span>|<span data-ttu-id="117c2-636">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-636">string</span></span>|<span data-ttu-id="117c2-637">是</span><span class="sxs-lookup"><span data-stu-id="117c2-637">Yes</span></span>|<span data-ttu-id="117c2-638">規則名稱，不包括訂用帳戶和主題名稱。</span><span class="sxs-lookup"><span data-stu-id="117c2-638">Rule name, not including subscription and topic names.</span></span>|  
|<span data-ttu-id="117c2-639">rule-description</span><span class="sxs-lookup"><span data-stu-id="117c2-639">rule-description</span></span>|<span data-ttu-id="117c2-640">map</span><span class="sxs-lookup"><span data-stu-id="117c2-640">map</span></span>|<span data-ttu-id="117c2-641">是</span><span class="sxs-lookup"><span data-stu-id="117c2-641">Yes</span></span>|<span data-ttu-id="117c2-642">如下一節中指定的規則描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-642">Rule description as specified in next section.</span></span>|  
  
<span data-ttu-id="117c2-643">**rule-description** 對應必須包含下列項目，當中 **sql-filter** 和 **correlation-filter** 為互斥：</span><span class="sxs-lookup"><span data-stu-id="117c2-643">The **rule-description** map must include the following entries, where **sql-filter** and **correlation-filter** are mutually exclusive:</span></span>  
  
|<span data-ttu-id="117c2-644">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-644">Key</span></span>|<span data-ttu-id="117c2-645">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-645">Value Type</span></span>|<span data-ttu-id="117c2-646">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-646">Required</span></span>|<span data-ttu-id="117c2-647">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-647">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-648">sql-filter</span><span class="sxs-lookup"><span data-stu-id="117c2-648">sql-filter</span></span>|<span data-ttu-id="117c2-649">map</span><span class="sxs-lookup"><span data-stu-id="117c2-649">map</span></span>|<span data-ttu-id="117c2-650">是</span><span class="sxs-lookup"><span data-stu-id="117c2-650">Yes</span></span>|<span data-ttu-id="117c2-651">`sql-filter`，如下一節中所指定。</span><span class="sxs-lookup"><span data-stu-id="117c2-651">`sql-filter`, as specified in the next section.</span></span>|  
|<span data-ttu-id="117c2-652">correlation-filter</span><span class="sxs-lookup"><span data-stu-id="117c2-652">correlation-filter</span></span>|<span data-ttu-id="117c2-653">map</span><span class="sxs-lookup"><span data-stu-id="117c2-653">map</span></span>|<span data-ttu-id="117c2-654">是</span><span class="sxs-lookup"><span data-stu-id="117c2-654">Yes</span></span>|<span data-ttu-id="117c2-655">`correlation-filter`，如下一節中所指定。</span><span class="sxs-lookup"><span data-stu-id="117c2-655">`correlation-filter`, as specified in the next section.</span></span>|  
|<span data-ttu-id="117c2-656">sql-rule-action</span><span class="sxs-lookup"><span data-stu-id="117c2-656">sql-rule-action</span></span>|<span data-ttu-id="117c2-657">map</span><span class="sxs-lookup"><span data-stu-id="117c2-657">map</span></span>|<span data-ttu-id="117c2-658">是</span><span class="sxs-lookup"><span data-stu-id="117c2-658">Yes</span></span>|<span data-ttu-id="117c2-659">`sql-rule-action`，如下一節中所指定。</span><span class="sxs-lookup"><span data-stu-id="117c2-659">`sql-rule-action`, as specified in the next section.</span></span>|  
  
<span data-ttu-id="117c2-660">sql-filter 對應必須包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="117c2-660">The sql-filter map must include the following entries:</span></span>  
  
|<span data-ttu-id="117c2-661">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-661">Key</span></span>|<span data-ttu-id="117c2-662">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-662">Value Type</span></span>|<span data-ttu-id="117c2-663">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-663">Required</span></span>|<span data-ttu-id="117c2-664">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-664">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-665">expression</span><span class="sxs-lookup"><span data-stu-id="117c2-665">expression</span></span>|<span data-ttu-id="117c2-666">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-666">string</span></span>|<span data-ttu-id="117c2-667">是</span><span class="sxs-lookup"><span data-stu-id="117c2-667">Yes</span></span>|<span data-ttu-id="117c2-668">Sql 篩選運算式。</span><span class="sxs-lookup"><span data-stu-id="117c2-668">Sql filter expression.</span></span>|  
  
<span data-ttu-id="117c2-669">**correlation-filter** 對應必須至少包含下列項目之一：</span><span class="sxs-lookup"><span data-stu-id="117c2-669">The **correlation-filter** map must include at least one of the following entries:</span></span>  
  
|<span data-ttu-id="117c2-670">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-670">Key</span></span>|<span data-ttu-id="117c2-671">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-671">Value Type</span></span>|<span data-ttu-id="117c2-672">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-672">Required</span></span>|<span data-ttu-id="117c2-673">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-673">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-674">correlation-id</span><span class="sxs-lookup"><span data-stu-id="117c2-674">correlation-id</span></span>|<span data-ttu-id="117c2-675">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-675">string</span></span>|<span data-ttu-id="117c2-676">否</span><span class="sxs-lookup"><span data-stu-id="117c2-676">No</span></span>||  
|<span data-ttu-id="117c2-677">message-id</span><span class="sxs-lookup"><span data-stu-id="117c2-677">message-id</span></span>|<span data-ttu-id="117c2-678">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-678">string</span></span>|<span data-ttu-id="117c2-679">否</span><span class="sxs-lookup"><span data-stu-id="117c2-679">No</span></span>||  
|<span data-ttu-id="117c2-680">to</span><span class="sxs-lookup"><span data-stu-id="117c2-680">to</span></span>|<span data-ttu-id="117c2-681">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-681">string</span></span>|<span data-ttu-id="117c2-682">否</span><span class="sxs-lookup"><span data-stu-id="117c2-682">No</span></span>||  
|<span data-ttu-id="117c2-683">reply-to</span><span class="sxs-lookup"><span data-stu-id="117c2-683">reply-to</span></span>|<span data-ttu-id="117c2-684">string</span><span class="sxs-lookup"><span data-stu-id="117c2-684">string</span></span>|<span data-ttu-id="117c2-685">否</span><span class="sxs-lookup"><span data-stu-id="117c2-685">No</span></span>||  
|<span data-ttu-id="117c2-686">標籤</span><span class="sxs-lookup"><span data-stu-id="117c2-686">label</span></span>|<span data-ttu-id="117c2-687">string</span><span class="sxs-lookup"><span data-stu-id="117c2-687">string</span></span>|<span data-ttu-id="117c2-688">否</span><span class="sxs-lookup"><span data-stu-id="117c2-688">No</span></span>||  
|<span data-ttu-id="117c2-689">session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-689">session-id</span></span>|<span data-ttu-id="117c2-690">string</span><span class="sxs-lookup"><span data-stu-id="117c2-690">string</span></span>|<span data-ttu-id="117c2-691">否</span><span class="sxs-lookup"><span data-stu-id="117c2-691">No</span></span>||  
|<span data-ttu-id="117c2-692">reply-to-session-id</span><span class="sxs-lookup"><span data-stu-id="117c2-692">reply-to-session-id</span></span>|<span data-ttu-id="117c2-693">string</span><span class="sxs-lookup"><span data-stu-id="117c2-693">string</span></span>|<span data-ttu-id="117c2-694">否</span><span class="sxs-lookup"><span data-stu-id="117c2-694">No</span></span>||  
|<span data-ttu-id="117c2-695">Content-Type</span><span class="sxs-lookup"><span data-stu-id="117c2-695">content-type</span></span>|<span data-ttu-id="117c2-696">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-696">string</span></span>|<span data-ttu-id="117c2-697">否</span><span class="sxs-lookup"><span data-stu-id="117c2-697">No</span></span>||  
|<span data-ttu-id="117c2-698">properties</span><span class="sxs-lookup"><span data-stu-id="117c2-698">properties</span></span>|<span data-ttu-id="117c2-699">map</span><span class="sxs-lookup"><span data-stu-id="117c2-699">map</span></span>|<span data-ttu-id="117c2-700">否</span><span class="sxs-lookup"><span data-stu-id="117c2-700">No</span></span>|<span data-ttu-id="117c2-701">對應至服務匯流排 [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties)。</span><span class="sxs-lookup"><span data-stu-id="117c2-701">Maps to Service Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).</span></span>|  
  
<span data-ttu-id="117c2-702">**sql-rule-action** 對應必須包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="117c2-702">The **sql-rule-action** map must include the following entries:</span></span>  
  
|<span data-ttu-id="117c2-703">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-703">Key</span></span>|<span data-ttu-id="117c2-704">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-704">Value Type</span></span>|<span data-ttu-id="117c2-705">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-705">Required</span></span>|<span data-ttu-id="117c2-706">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-706">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-707">expression</span><span class="sxs-lookup"><span data-stu-id="117c2-707">expression</span></span>|<span data-ttu-id="117c2-708">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-708">string</span></span>|<span data-ttu-id="117c2-709">是</span><span class="sxs-lookup"><span data-stu-id="117c2-709">Yes</span></span>|<span data-ttu-id="117c2-710">Sql 動作運算式。</span><span class="sxs-lookup"><span data-stu-id="117c2-710">Sql action expression.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-711">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-711">Response</span></span>  

<span data-ttu-id="117c2-712">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-712">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-713">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-713">Key</span></span>|<span data-ttu-id="117c2-714">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-714">Value Type</span></span>|<span data-ttu-id="117c2-715">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-715">Required</span></span>|<span data-ttu-id="117c2-716">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-716">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-717">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-717">statusCode</span></span>|<span data-ttu-id="117c2-718">int</span><span class="sxs-lookup"><span data-stu-id="117c2-718">int</span></span>|<span data-ttu-id="117c2-719">是</span><span class="sxs-lookup"><span data-stu-id="117c2-719">Yes</span></span>|<span data-ttu-id="117c2-720">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-720">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-721">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="117c2-721">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="117c2-722">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-722">statusDescription</span></span>|<span data-ttu-id="117c2-723">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-723">string</span></span>|<span data-ttu-id="117c2-724">否</span><span class="sxs-lookup"><span data-stu-id="117c2-724">No</span></span>|<span data-ttu-id="117c2-725">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-725">Description of the status.</span></span>|  
  
### <a name="remove-rule"></a><span data-ttu-id="117c2-726">移除規則</span><span class="sxs-lookup"><span data-stu-id="117c2-726">Remove Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-727">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-727">Request</span></span>  

<span data-ttu-id="117c2-728">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-728">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-729">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-729">Key</span></span>|<span data-ttu-id="117c2-730">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-730">Value Type</span></span>|<span data-ttu-id="117c2-731">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-731">Required</span></span>|<span data-ttu-id="117c2-732">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-732">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-733">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-733">operation</span></span>|<span data-ttu-id="117c2-734">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-734">string</span></span>|<span data-ttu-id="117c2-735">是</span><span class="sxs-lookup"><span data-stu-id="117c2-735">Yes</span></span>|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-736">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-736">uint</span></span>|<span data-ttu-id="117c2-737">否</span><span class="sxs-lookup"><span data-stu-id="117c2-737">No</span></span>|<span data-ttu-id="117c2-738">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-738">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-739">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-739">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-740">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-740">Key</span></span>|<span data-ttu-id="117c2-741">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-741">Value Type</span></span>|<span data-ttu-id="117c2-742">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-742">Required</span></span>|<span data-ttu-id="117c2-743">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-743">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-744">rule-name</span><span class="sxs-lookup"><span data-stu-id="117c2-744">rule-name</span></span>|<span data-ttu-id="117c2-745">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-745">string</span></span>|<span data-ttu-id="117c2-746">是</span><span class="sxs-lookup"><span data-stu-id="117c2-746">Yes</span></span>|<span data-ttu-id="117c2-747">規則名稱，不包括訂用帳戶和主題名稱。</span><span class="sxs-lookup"><span data-stu-id="117c2-747">Rule name, not including subscription and topic names.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-748">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-748">Response</span></span>  

<span data-ttu-id="117c2-749">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-749">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-750">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-750">Key</span></span>|<span data-ttu-id="117c2-751">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-751">Value Type</span></span>|<span data-ttu-id="117c2-752">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-752">Required</span></span>|<span data-ttu-id="117c2-753">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-753">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-754">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-754">statusCode</span></span>|<span data-ttu-id="117c2-755">int</span><span class="sxs-lookup"><span data-stu-id="117c2-755">int</span></span>|<span data-ttu-id="117c2-756">是</span><span class="sxs-lookup"><span data-stu-id="117c2-756">Yes</span></span>|<span data-ttu-id="117c2-757">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-757">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-758">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="117c2-758">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="117c2-759">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-759">statusDescription</span></span>|<span data-ttu-id="117c2-760">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-760">string</span></span>|<span data-ttu-id="117c2-761">否</span><span class="sxs-lookup"><span data-stu-id="117c2-761">No</span></span>|<span data-ttu-id="117c2-762">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-762">Description of the status.</span></span>|  
  
## <a name="deferred-message-operations"></a><span data-ttu-id="117c2-763">延遲的訊息作業</span><span class="sxs-lookup"><span data-stu-id="117c2-763">Deferred message operations</span></span>  
  
### <a name="receive-by-sequence-number"></a><span data-ttu-id="117c2-764">依照序號接收</span><span class="sxs-lookup"><span data-stu-id="117c2-764">Receive by sequence number</span></span>  

<span data-ttu-id="117c2-765">依序號接收延遲的訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-765">Receives deferred messages by sequence number.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-766">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-766">Request</span></span>  

<span data-ttu-id="117c2-767">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-767">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-768">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-768">Key</span></span>|<span data-ttu-id="117c2-769">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-769">Value Type</span></span>|<span data-ttu-id="117c2-770">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-770">Required</span></span>|<span data-ttu-id="117c2-771">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-771">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-772">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-772">operation</span></span>|<span data-ttu-id="117c2-773">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-773">string</span></span>|<span data-ttu-id="117c2-774">是</span><span class="sxs-lookup"><span data-stu-id="117c2-774">Yes</span></span>|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-775">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-775">uint</span></span>|<span data-ttu-id="117c2-776">否</span><span class="sxs-lookup"><span data-stu-id="117c2-776">No</span></span>|<span data-ttu-id="117c2-777">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-777">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-778">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-778">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-779">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-779">Key</span></span>|<span data-ttu-id="117c2-780">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-780">Value Type</span></span>|<span data-ttu-id="117c2-781">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-781">Required</span></span>|<span data-ttu-id="117c2-782">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-782">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-783">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="117c2-783">sequence-numbers</span></span>|<span data-ttu-id="117c2-784">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-784">array of long</span></span>|<span data-ttu-id="117c2-785">是</span><span class="sxs-lookup"><span data-stu-id="117c2-785">Yes</span></span>|<span data-ttu-id="117c2-786">序號。</span><span class="sxs-lookup"><span data-stu-id="117c2-786">Sequence numbers.</span></span>|  
|<span data-ttu-id="117c2-787">receiver-settle-mode</span><span class="sxs-lookup"><span data-stu-id="117c2-787">receiver-settle-mode</span></span>|<span data-ttu-id="117c2-788">ubyte</span><span class="sxs-lookup"><span data-stu-id="117c2-788">ubyte</span></span>|<span data-ttu-id="117c2-789">是</span><span class="sxs-lookup"><span data-stu-id="117c2-789">Yes</span></span>|<span data-ttu-id="117c2-790">AMQP 核心 1.0 版中所指定的「收件者支付」模式。</span><span class="sxs-lookup"><span data-stu-id="117c2-790">**Receiver settle** mode as specified in AMQP core v1.0.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-791">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-791">Response</span></span>  

<span data-ttu-id="117c2-792">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-792">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-793">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-793">Key</span></span>|<span data-ttu-id="117c2-794">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-794">Value Type</span></span>|<span data-ttu-id="117c2-795">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-795">Required</span></span>|<span data-ttu-id="117c2-796">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-796">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-797">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-797">statusCode</span></span>|<span data-ttu-id="117c2-798">int</span><span class="sxs-lookup"><span data-stu-id="117c2-798">int</span></span>|<span data-ttu-id="117c2-799">是</span><span class="sxs-lookup"><span data-stu-id="117c2-799">Yes</span></span>|<span data-ttu-id="117c2-800">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-800">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-801">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="117c2-801">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="117c2-802">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-802">statusDescription</span></span>|<span data-ttu-id="117c2-803">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-803">string</span></span>|<span data-ttu-id="117c2-804">否</span><span class="sxs-lookup"><span data-stu-id="117c2-804">No</span></span>|<span data-ttu-id="117c2-805">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-805">Description of the status.</span></span>|  
  
<span data-ttu-id="117c2-806">回應訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-806">The response message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-807">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-807">Key</span></span>|<span data-ttu-id="117c2-808">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-808">Value Type</span></span>|<span data-ttu-id="117c2-809">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-809">Required</span></span>|<span data-ttu-id="117c2-810">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-810">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-811">上限</span><span class="sxs-lookup"><span data-stu-id="117c2-811">messages</span></span>|<span data-ttu-id="117c2-812">對應的清單</span><span class="sxs-lookup"><span data-stu-id="117c2-812">list of maps</span></span>|<span data-ttu-id="117c2-813">是</span><span class="sxs-lookup"><span data-stu-id="117c2-813">Yes</span></span>|<span data-ttu-id="117c2-814">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="117c2-814">List of messages where every map represents a message.</span></span>|  
  
<span data-ttu-id="117c2-815">代表訊息的對應必須包含下列項目：</span><span class="sxs-lookup"><span data-stu-id="117c2-815">The map representing a message must contain the following entries:</span></span>  
  
|<span data-ttu-id="117c2-816">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-816">Key</span></span>|<span data-ttu-id="117c2-817">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-817">Value Type</span></span>|<span data-ttu-id="117c2-818">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-818">Required</span></span>|<span data-ttu-id="117c2-819">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-819">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-820">lock-token</span><span class="sxs-lookup"><span data-stu-id="117c2-820">lock-token</span></span>|<span data-ttu-id="117c2-821">uuid</span><span class="sxs-lookup"><span data-stu-id="117c2-821">uuid</span></span>|<span data-ttu-id="117c2-822">是</span><span class="sxs-lookup"><span data-stu-id="117c2-822">Yes</span></span>|<span data-ttu-id="117c2-823">如果 `receiver-settle-mode` 為 1 則鎖定權杖。</span><span class="sxs-lookup"><span data-stu-id="117c2-823">Lock token if `receiver-settle-mode` is 1.</span></span>|  
|<span data-ttu-id="117c2-824">訊息</span><span class="sxs-lookup"><span data-stu-id="117c2-824">message</span></span>|<span data-ttu-id="117c2-825">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-825">array of byte</span></span>|<span data-ttu-id="117c2-826">是</span><span class="sxs-lookup"><span data-stu-id="117c2-826">Yes</span></span>|<span data-ttu-id="117c2-827">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="117c2-827">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="update-disposition-status"></a><span data-ttu-id="117c2-828">更新配置狀態</span><span class="sxs-lookup"><span data-stu-id="117c2-828">Update disposition status</span></span>  

<span data-ttu-id="117c2-829">更新延遲訊息的配置狀態。</span><span class="sxs-lookup"><span data-stu-id="117c2-829">Updates the disposition status of deferred messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="117c2-830">要求</span><span class="sxs-lookup"><span data-stu-id="117c2-830">Request</span></span>  

<span data-ttu-id="117c2-831">要求訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-831">The request message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-832">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-832">Key</span></span>|<span data-ttu-id="117c2-833">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-833">Value Type</span></span>|<span data-ttu-id="117c2-834">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-834">Required</span></span>|<span data-ttu-id="117c2-835">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-835">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-836">operation</span><span class="sxs-lookup"><span data-stu-id="117c2-836">operation</span></span>|<span data-ttu-id="117c2-837">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-837">string</span></span>|<span data-ttu-id="117c2-838">是</span><span class="sxs-lookup"><span data-stu-id="117c2-838">Yes</span></span>|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="117c2-839">uint</span><span class="sxs-lookup"><span data-stu-id="117c2-839">uint</span></span>|<span data-ttu-id="117c2-840">否</span><span class="sxs-lookup"><span data-stu-id="117c2-840">No</span></span>|<span data-ttu-id="117c2-841">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="117c2-841">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="117c2-842">要求訊息本文必須由包含**對應**與下列項目的 **amqp-value** 區段所組成：</span><span class="sxs-lookup"><span data-stu-id="117c2-842">The request message body must consist of an **amqp-value** section containing a **map** with the following entries:</span></span>  
  
|<span data-ttu-id="117c2-843">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-843">Key</span></span>|<span data-ttu-id="117c2-844">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-844">Value Type</span></span>|<span data-ttu-id="117c2-845">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-845">Required</span></span>|<span data-ttu-id="117c2-846">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-846">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-847">disposition-status</span><span class="sxs-lookup"><span data-stu-id="117c2-847">disposition-status</span></span>|<span data-ttu-id="117c2-848">string</span><span class="sxs-lookup"><span data-stu-id="117c2-848">string</span></span>|<span data-ttu-id="117c2-849">是</span><span class="sxs-lookup"><span data-stu-id="117c2-849">Yes</span></span>|<span data-ttu-id="117c2-850">完成</span><span class="sxs-lookup"><span data-stu-id="117c2-850">completed</span></span><br /><br /> <span data-ttu-id="117c2-851">放棄</span><span class="sxs-lookup"><span data-stu-id="117c2-851">abandoned</span></span><br /><br /> <span data-ttu-id="117c2-852">暫止</span><span class="sxs-lookup"><span data-stu-id="117c2-852">suspended</span></span>|  
|<span data-ttu-id="117c2-853">lock-tokens</span><span class="sxs-lookup"><span data-stu-id="117c2-853">lock-tokens</span></span>|<span data-ttu-id="117c2-854">UUID 的陣列</span><span class="sxs-lookup"><span data-stu-id="117c2-854">array of uuid</span></span>|<span data-ttu-id="117c2-855">是</span><span class="sxs-lookup"><span data-stu-id="117c2-855">Yes</span></span>|<span data-ttu-id="117c2-856">要更新配置狀態的訊息鎖定權杖。</span><span class="sxs-lookup"><span data-stu-id="117c2-856">Message lock tokens to update disposition status.</span></span>|  
|<span data-ttu-id="117c2-857">deadletter-reason</span><span class="sxs-lookup"><span data-stu-id="117c2-857">deadletter-reason</span></span>|<span data-ttu-id="117c2-858">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-858">string</span></span>|<span data-ttu-id="117c2-859">否</span><span class="sxs-lookup"><span data-stu-id="117c2-859">No</span></span>|<span data-ttu-id="117c2-860">如果配置狀態設定為 **暫停** 則可能會設定。</span><span class="sxs-lookup"><span data-stu-id="117c2-860">May be set if disposition status is set to **suspended**.</span></span>|  
|<span data-ttu-id="117c2-861">deadletter-description</span><span class="sxs-lookup"><span data-stu-id="117c2-861">deadletter-description</span></span>|<span data-ttu-id="117c2-862">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-862">string</span></span>|<span data-ttu-id="117c2-863">否</span><span class="sxs-lookup"><span data-stu-id="117c2-863">No</span></span>|<span data-ttu-id="117c2-864">如果配置狀態設定為 **暫停** 則可能會設定。</span><span class="sxs-lookup"><span data-stu-id="117c2-864">May be set if disposition status is set to **suspended**.</span></span>|  
|<span data-ttu-id="117c2-865">properties-to-modify</span><span class="sxs-lookup"><span data-stu-id="117c2-865">properties-to-modify</span></span>|<span data-ttu-id="117c2-866">map</span><span class="sxs-lookup"><span data-stu-id="117c2-866">map</span></span>|<span data-ttu-id="117c2-867">否</span><span class="sxs-lookup"><span data-stu-id="117c2-867">No</span></span>|<span data-ttu-id="117c2-868">要修改的服務匯流排代理訊息屬性清單。</span><span class="sxs-lookup"><span data-stu-id="117c2-868">List of Service Bus brokered message properties to modify.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="117c2-869">Response</span><span class="sxs-lookup"><span data-stu-id="117c2-869">Response</span></span>  

<span data-ttu-id="117c2-870">回應訊息必須包含下列應用程式屬性：</span><span class="sxs-lookup"><span data-stu-id="117c2-870">The response message must include the following application properties:</span></span>  
  
|<span data-ttu-id="117c2-871">金鑰</span><span class="sxs-lookup"><span data-stu-id="117c2-871">Key</span></span>|<span data-ttu-id="117c2-872">值類型</span><span class="sxs-lookup"><span data-stu-id="117c2-872">Value Type</span></span>|<span data-ttu-id="117c2-873">必要</span><span class="sxs-lookup"><span data-stu-id="117c2-873">Required</span></span>|<span data-ttu-id="117c2-874">值內容</span><span class="sxs-lookup"><span data-stu-id="117c2-874">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="117c2-875">StatusCode</span><span class="sxs-lookup"><span data-stu-id="117c2-875">statusCode</span></span>|<span data-ttu-id="117c2-876">int</span><span class="sxs-lookup"><span data-stu-id="117c2-876">int</span></span>|<span data-ttu-id="117c2-877">是</span><span class="sxs-lookup"><span data-stu-id="117c2-877">Yes</span></span>|<span data-ttu-id="117c2-878">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="117c2-878">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="117c2-879">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="117c2-879">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="117c2-880">statusDescription</span><span class="sxs-lookup"><span data-stu-id="117c2-880">statusDescription</span></span>|<span data-ttu-id="117c2-881">字串</span><span class="sxs-lookup"><span data-stu-id="117c2-881">string</span></span>|<span data-ttu-id="117c2-882">否</span><span class="sxs-lookup"><span data-stu-id="117c2-882">No</span></span>|<span data-ttu-id="117c2-883">狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="117c2-883">Description of the status.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="117c2-884">後續步驟</span><span class="sxs-lookup"><span data-stu-id="117c2-884">Next steps</span></span>

<span data-ttu-id="117c2-885">若要深入了解 AMQP 和服務匯流排，請造訪下列連結：</span><span class="sxs-lookup"><span data-stu-id="117c2-885">To learn more about AMQP and Service Bus, visit the following links:</span></span>

* <span data-ttu-id="117c2-886">[服務匯流排 AMQP 概觀]</span><span class="sxs-lookup"><span data-stu-id="117c2-886">[Service Bus AMQP overview]</span></span>
* <span data-ttu-id="117c2-887">[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]</span><span class="sxs-lookup"><span data-stu-id="117c2-887">[AMQP 1.0 support for Service Bus partitioned queues and topics]</span></span>
* <span data-ttu-id="117c2-888">[Windows Server 服務匯流排中的 AMQP]</span><span class="sxs-lookup"><span data-stu-id="117c2-888">[AMQP in Service Bus for Windows Server]</span></span>

<span data-ttu-id="117c2-889">[服務匯流排 AMQP 概觀]: service-bus-amqp-overview.md</span><span class="sxs-lookup"><span data-stu-id="117c2-889">[Service Bus AMQP overview]: service-bus-amqp-overview.md</span></span>
<span data-ttu-id="117c2-890">[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]: service-bus-partitioned-queues-and-topics-amqp-overview.md</span><span class="sxs-lookup"><span data-stu-id="117c2-890">[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md</span></span>
<span data-ttu-id="117c2-891">[Windows Server 服務匯流排中的 AMQP]: https://msdn.microsoft.com/library/dn574799.asp</span><span class="sxs-lookup"><span data-stu-id="117c2-891">[AMQP in Service Bus for Windows Server]: https://msdn.microsoft.com/library/dn574799.asp</span></span>