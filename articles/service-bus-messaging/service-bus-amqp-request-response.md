---
title: "Azure 服務匯流排要求-回應為基礎的作業中 aaaAMQP 1.0 |Microsoft 文件"
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
ms.openlocfilehash: e4f26219c53b0c4172747af683fe511d6366ff2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="amqp-10-in-microsoft-azure-service-bus-request-response-based-operations"></a><span data-ttu-id="da147-103">Microsoft Azure 服務匯流排中的 AMQP 1.0：要求/回應架構作業</span><span class="sxs-lookup"><span data-stu-id="da147-103">AMQP 1.0 in Microsoft Azure Service Bus: request-response-based operations</span></span>

<span data-ttu-id="da147-104">本主題會定義 Microsoft Azure 服務匯流排要求/回應架構作業 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="da147-104">This topic defines hello list of Microsoft Azure Service Bus request/response-based operations.</span></span> <span data-ttu-id="da147-105">這項資訊根據 hello AMQP 管理版本 1.0 工作草稿。</span><span class="sxs-lookup"><span data-stu-id="da147-105">This information is based on hello AMQP Management Version 1.0 working draft.</span></span>  
  
<span data-ttu-id="da147-106">詳細的有線等級 AMQP 1.0 通訊協定指引，其中說明如何實作服務匯流排，和 hello OASIS AMQP 技術規格為基礎，請參閱 hello [Azure 服務匯流排和事件中心的通訊協定指南中的 AMQP 1.0](service-bus-amqp-protocol-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="da147-106">For a detailed wire-level AMQP 1.0 protocol guide, which explains how Service Bus implements and builds on hello OASIS AMQP technical specification, see hello [AMQP 1.0 in Azure Service Bus and Event Hubs protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="concepts"></a><span data-ttu-id="da147-107">概念</span><span class="sxs-lookup"><span data-stu-id="da147-107">Concepts</span></span>  
  
### <a name="entity-description"></a><span data-ttu-id="da147-108">實體描述</span><span class="sxs-lookup"><span data-stu-id="da147-108">Entity description</span></span>  

<span data-ttu-id="da147-109">實體描述是指 Service Bus tooeither [QueueDescription 類別](/dotnet/api/microsoft.servicebus.messaging.queuedescription)， [TopicDescription 類別](/dotnet/api/microsoft.servicebus.messaging.topicdescription)，或[SubscriptionDescription 類別](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription)物件。</span><span class="sxs-lookup"><span data-stu-id="da147-109">An entity description refers tooeither a Service Bus [QueueDescription Class](/dotnet/api/microsoft.servicebus.messaging.queuedescription), [TopicDescription Class](/dotnet/api/microsoft.servicebus.messaging.topicdescription), or [SubscriptionDescription Class](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription) object.</span></span>  
  
### <a name="brokered-message"></a><span data-ttu-id="da147-110">代理訊息</span><span class="sxs-lookup"><span data-stu-id="da147-110">Brokered message</span></span>  

<span data-ttu-id="da147-111">表示服務匯流排，也就是對應的 tooan AMQP 訊息中的訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-111">Represents a message in Service Bus, which is mapped tooan AMQP message.</span></span> <span data-ttu-id="da147-112">hello 對應定義於 hello[服務匯流排 AMQP 通訊協定指南](service-bus-amqp-protocol-guide.md)。</span><span class="sxs-lookup"><span data-stu-id="da147-112">hello mapping is defined in hello [Service Bus AMQP protocol guide](service-bus-amqp-protocol-guide.md).</span></span>  
  
## <a name="attach-tooentity-management-node"></a><span data-ttu-id="da147-113">附加 tooentity 管理節點</span><span class="sxs-lookup"><span data-stu-id="da147-113">Attach tooentity management node</span></span>  

<span data-ttu-id="da147-114">這份文件中所述的所有 hello 作業會遵循要求/回應模式，已設定領域的 tooan 實體，但需要附加 tooan 實體管理節點。</span><span class="sxs-lookup"><span data-stu-id="da147-114">All hello operations described in this document follow a request/response pattern, are scoped tooan entity, and require attaching tooan entity management node.</span></span>  
  
### <a name="create-link-for-sending-requests"></a><span data-ttu-id="da147-115">建立傳送要求的連結</span><span class="sxs-lookup"><span data-stu-id="da147-115">Create link for sending requests</span></span>  

<span data-ttu-id="da147-116">建立傳送要求的連結 toohello 管理節點。</span><span class="sxs-lookup"><span data-stu-id="da147-116">Creates a link toohello management node for sending requests.</span></span>  
  
```  
requestLink = session.attach(     
role: SENDER,   
    target: { address: "<entity address>/$management" },   
    source: { address: ""<my request link unique address>" }   
)  
  
```  
  
### <a name="create-link-for-receiving-responses"></a><span data-ttu-id="da147-117">建立接收回應的連結</span><span class="sxs-lookup"><span data-stu-id="da147-117">Create link for receiving responses</span></span>  

<span data-ttu-id="da147-118">建立接收回應從 hello 管理節點的連結。</span><span class="sxs-lookup"><span data-stu-id="da147-118">Creates a link for receiving responses from hello management node.</span></span>  
  
```  
responseLink = session.attach(    
role: RECEIVER,   
    source: { address: "<entity address>/$management" }   
    target: { address: "<my response link unique address>" }   
)  
  
```  
  
### <a name="transfer-a-request-message"></a><span data-ttu-id="da147-119">傳輸要求訊息</span><span class="sxs-lookup"><span data-stu-id="da147-119">Transfer a request message</span></span>  

<span data-ttu-id="da147-120">傳輸要求訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-120">Transfers a request message.</span></span>  
  
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
  
### <a name="receive-a-response-message"></a><span data-ttu-id="da147-121">接收回應訊息</span><span class="sxs-lookup"><span data-stu-id="da147-121">Receive a response message</span></span>  

<span data-ttu-id="da147-122">接收來自 hello 回應連結 hello 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-122">Receives hello response message from hello response link.</span></span>  
  
```  
responseMessage = responseLink.receiveTransfer()  
```  
  
<span data-ttu-id="da147-123">hello 回應訊息處於下列表單的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-123">hello response message is in hello following form:</span></span>
  
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
  
### <a name="service-bus-entity-address"></a><span data-ttu-id="da147-124">服務匯流排實體位址</span><span class="sxs-lookup"><span data-stu-id="da147-124">Service Bus entity address</span></span>  

<span data-ttu-id="da147-125">必須處理服務匯流排實體，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="da147-125">Service Bus entities must be addressed as follows:</span></span>  
  
|<span data-ttu-id="da147-126">實體類型</span><span class="sxs-lookup"><span data-stu-id="da147-126">Entity type</span></span>|<span data-ttu-id="da147-127">位址</span><span class="sxs-lookup"><span data-stu-id="da147-127">Address</span></span>|<span data-ttu-id="da147-128">範例</span><span class="sxs-lookup"><span data-stu-id="da147-128">Example</span></span>|  
|-----------------|-------------|-------------|  
|<span data-ttu-id="da147-129">佇列</span><span class="sxs-lookup"><span data-stu-id="da147-129">queue</span></span>|`<queue_name>`|`“myQueue”`<br /><br /> `“site1/myQueue”`|  
|<span data-ttu-id="da147-130">主題</span><span class="sxs-lookup"><span data-stu-id="da147-130">topic</span></span>|`<topic_name>`|`“myTopic”`<br /><br /> `“site2/page1/myQueue”`|  
|<span data-ttu-id="da147-131">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="da147-131">subscription</span></span>|`<topic_name>/Subscriptions/<subscription_name>`|`“myTopic/Subscriptions/MySub”`|  
  
## <a name="message-operations"></a><span data-ttu-id="da147-132">訊息作業</span><span class="sxs-lookup"><span data-stu-id="da147-132">Message operations</span></span>  
  
### <a name="message-renew-lock"></a><span data-ttu-id="da147-133">訊息更新鎖定</span><span class="sxs-lookup"><span data-stu-id="da147-133">Message Renew Lock</span></span>  

<span data-ttu-id="da147-134">延伸 hello 鎖定訊息的 hello hello 實體描述中指定的時間。</span><span class="sxs-lookup"><span data-stu-id="da147-134">Extends hello lock of a message by hello time specified in hello entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-135">要求</span><span class="sxs-lookup"><span data-stu-id="da147-135">Request</span></span>  

<span data-ttu-id="da147-136">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-136">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-137">Key</span><span class="sxs-lookup"><span data-stu-id="da147-137">Key</span></span>|<span data-ttu-id="da147-138">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-138">Value Type</span></span>|<span data-ttu-id="da147-139">必要</span><span class="sxs-lookup"><span data-stu-id="da147-139">Required</span></span>|<span data-ttu-id="da147-140">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-140">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-141">operation</span><span class="sxs-lookup"><span data-stu-id="da147-141">operation</span></span>|<span data-ttu-id="da147-142">字串</span><span class="sxs-lookup"><span data-stu-id="da147-142">string</span></span>|<span data-ttu-id="da147-143">是</span><span class="sxs-lookup"><span data-stu-id="da147-143">Yes</span></span>|`com.microsoft:renew-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-144">uint</span><span class="sxs-lookup"><span data-stu-id="da147-144">uint</span></span>|<span data-ttu-id="da147-145">否</span><span class="sxs-lookup"><span data-stu-id="da147-145">No</span></span>|<span data-ttu-id="da147-146">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-146">Operation server timeout in milliseconds.</span></span>|  
  
 <span data-ttu-id="da147-147">以下列項目 hello 含有對應的 amqp 值區段必須包含 hello 要求訊息內文：</span><span class="sxs-lookup"><span data-stu-id="da147-147">hello request message body must consist of an amqp-value section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-148">Key</span><span class="sxs-lookup"><span data-stu-id="da147-148">Key</span></span>|<span data-ttu-id="da147-149">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-149">Value Type</span></span>|<span data-ttu-id="da147-150">必要</span><span class="sxs-lookup"><span data-stu-id="da147-150">Required</span></span>|<span data-ttu-id="da147-151">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-151">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`lock-tokens`|<span data-ttu-id="da147-152">UUID 的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-152">array of uuid</span></span>|<span data-ttu-id="da147-153">是</span><span class="sxs-lookup"><span data-stu-id="da147-153">Yes</span></span>|<span data-ttu-id="da147-154">訊息鎖定權杖 toorenew。</span><span class="sxs-lookup"><span data-stu-id="da147-154">Message lock tokens toorenew.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-155">Response</span><span class="sxs-lookup"><span data-stu-id="da147-155">Response</span></span>  

<span data-ttu-id="da147-156">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-156">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-157">Key</span><span class="sxs-lookup"><span data-stu-id="da147-157">Key</span></span>|<span data-ttu-id="da147-158">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-158">Value Type</span></span>|<span data-ttu-id="da147-159">必要</span><span class="sxs-lookup"><span data-stu-id="da147-159">Required</span></span>|<span data-ttu-id="da147-160">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-160">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-161">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-161">statusCode</span></span>|<span data-ttu-id="da147-162">int</span><span class="sxs-lookup"><span data-stu-id="da147-162">int</span></span>|<span data-ttu-id="da147-163">是</span><span class="sxs-lookup"><span data-stu-id="da147-163">Yes</span></span>|<span data-ttu-id="da147-164">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-164">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-165">200：確定 – 成功，否則失敗。</span><span class="sxs-lookup"><span data-stu-id="da147-165">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="da147-166">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-166">statusDescription</span></span>|<span data-ttu-id="da147-167">字串</span><span class="sxs-lookup"><span data-stu-id="da147-167">string</span></span>|<span data-ttu-id="da147-168">否</span><span class="sxs-lookup"><span data-stu-id="da147-168">No</span></span>|<span data-ttu-id="da147-169">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-169">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-170">以下列項目 hello 含有對應的 amqp 值區段必須包含 hello 回應訊息內文：</span><span class="sxs-lookup"><span data-stu-id="da147-170">hello response message body must consist of an amqp-value section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-171">Key</span><span class="sxs-lookup"><span data-stu-id="da147-171">Key</span></span>|<span data-ttu-id="da147-172">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-172">Value Type</span></span>|<span data-ttu-id="da147-173">必要</span><span class="sxs-lookup"><span data-stu-id="da147-173">Required</span></span>|<span data-ttu-id="da147-174">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-174">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-175">到期日</span><span class="sxs-lookup"><span data-stu-id="da147-175">expirations</span></span>|<span data-ttu-id="da147-176">時間戳記的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-176">array of timestamp</span></span>|<span data-ttu-id="da147-177">是</span><span class="sxs-lookup"><span data-stu-id="da147-177">Yes</span></span>|<span data-ttu-id="da147-178">訊息鎖定權杖新到期對應 toohello 要求鎖定權杖。</span><span class="sxs-lookup"><span data-stu-id="da147-178">Message lock token new expiration corresponding toohello request lock tokens.</span></span>|  
  
### <a name="peek-message"></a><span data-ttu-id="da147-179">查看訊息</span><span class="sxs-lookup"><span data-stu-id="da147-179">Peek Message</span></span>  

<span data-ttu-id="da147-180">查看訊息而不用鎖定。</span><span class="sxs-lookup"><span data-stu-id="da147-180">Peeks messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-181">要求</span><span class="sxs-lookup"><span data-stu-id="da147-181">Request</span></span>  

<span data-ttu-id="da147-182">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-182">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-183">Key</span><span class="sxs-lookup"><span data-stu-id="da147-183">Key</span></span>|<span data-ttu-id="da147-184">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-184">Value Type</span></span>|<span data-ttu-id="da147-185">必要</span><span class="sxs-lookup"><span data-stu-id="da147-185">Required</span></span>|<span data-ttu-id="da147-186">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-186">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-187">operation</span><span class="sxs-lookup"><span data-stu-id="da147-187">operation</span></span>|<span data-ttu-id="da147-188">字串</span><span class="sxs-lookup"><span data-stu-id="da147-188">string</span></span>|<span data-ttu-id="da147-189">是</span><span class="sxs-lookup"><span data-stu-id="da147-189">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-190">uint</span><span class="sxs-lookup"><span data-stu-id="da147-190">uint</span></span>|<span data-ttu-id="da147-191">否</span><span class="sxs-lookup"><span data-stu-id="da147-191">No</span></span>|<span data-ttu-id="da147-192">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-192">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-193">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-193">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-194">Key</span><span class="sxs-lookup"><span data-stu-id="da147-194">Key</span></span>|<span data-ttu-id="da147-195">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-195">Value Type</span></span>|<span data-ttu-id="da147-196">必要</span><span class="sxs-lookup"><span data-stu-id="da147-196">Required</span></span>|<span data-ttu-id="da147-197">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-197">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|`from-sequence-number`|<span data-ttu-id="da147-198">long</span><span class="sxs-lookup"><span data-stu-id="da147-198">long</span></span>|<span data-ttu-id="da147-199">是</span><span class="sxs-lookup"><span data-stu-id="da147-199">Yes</span></span>|<span data-ttu-id="da147-200">從哪些 toostart 查看的序號。</span><span class="sxs-lookup"><span data-stu-id="da147-200">Sequence number from which toostart peek.</span></span>|  
|`message-count`|<span data-ttu-id="da147-201">int</span><span class="sxs-lookup"><span data-stu-id="da147-201">int</span></span>|<span data-ttu-id="da147-202">是</span><span class="sxs-lookup"><span data-stu-id="da147-202">Yes</span></span>|<span data-ttu-id="da147-203">訊息 toopeek 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="da147-203">Maximum number of messages toopeek.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-204">Response</span><span class="sxs-lookup"><span data-stu-id="da147-204">Response</span></span>  

<span data-ttu-id="da147-205">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-205">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-206">Key</span><span class="sxs-lookup"><span data-stu-id="da147-206">Key</span></span>|<span data-ttu-id="da147-207">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-207">Value Type</span></span>|<span data-ttu-id="da147-208">必要</span><span class="sxs-lookup"><span data-stu-id="da147-208">Required</span></span>|<span data-ttu-id="da147-209">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-209">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-210">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-210">statusCode</span></span>|<span data-ttu-id="da147-211">int</span><span class="sxs-lookup"><span data-stu-id="da147-211">int</span></span>|<span data-ttu-id="da147-212">是</span><span class="sxs-lookup"><span data-stu-id="da147-212">Yes</span></span>|<span data-ttu-id="da147-213">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-213">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-214">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="da147-214">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="da147-215">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="da147-215">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="da147-216">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-216">statusDescription</span></span>|<span data-ttu-id="da147-217">字串</span><span class="sxs-lookup"><span data-stu-id="da147-217">string</span></span>|<span data-ttu-id="da147-218">否</span><span class="sxs-lookup"><span data-stu-id="da147-218">No</span></span>|<span data-ttu-id="da147-219">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-219">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-220">hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-220">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-221">Key</span><span class="sxs-lookup"><span data-stu-id="da147-221">Key</span></span>|<span data-ttu-id="da147-222">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-222">Value Type</span></span>|<span data-ttu-id="da147-223">必要</span><span class="sxs-lookup"><span data-stu-id="da147-223">Required</span></span>|<span data-ttu-id="da147-224">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-224">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-225">上限</span><span class="sxs-lookup"><span data-stu-id="da147-225">messages</span></span>|<span data-ttu-id="da147-226">對應的清單</span><span class="sxs-lookup"><span data-stu-id="da147-226">list of maps</span></span>|<span data-ttu-id="da147-227">是</span><span class="sxs-lookup"><span data-stu-id="da147-227">Yes</span></span>|<span data-ttu-id="da147-228">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="da147-228">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="da147-229">hello 對應表示訊息必須包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-229">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="da147-230">Key</span><span class="sxs-lookup"><span data-stu-id="da147-230">Key</span></span>|<span data-ttu-id="da147-231">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-231">Value Type</span></span>|<span data-ttu-id="da147-232">必要</span><span class="sxs-lookup"><span data-stu-id="da147-232">Required</span></span>|<span data-ttu-id="da147-233">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-233">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-234">訊息</span><span class="sxs-lookup"><span data-stu-id="da147-234">message</span></span>|<span data-ttu-id="da147-235">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-235">array of byte</span></span>|<span data-ttu-id="da147-236">是</span><span class="sxs-lookup"><span data-stu-id="da147-236">Yes</span></span>|<span data-ttu-id="da147-237">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-237">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="schedule-message"></a><span data-ttu-id="da147-238">排程訊息</span><span class="sxs-lookup"><span data-stu-id="da147-238">Schedule Message</span></span>  

<span data-ttu-id="da147-239">排程訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-239">Schedules messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-240">要求</span><span class="sxs-lookup"><span data-stu-id="da147-240">Request</span></span>  

<span data-ttu-id="da147-241">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-241">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-242">Key</span><span class="sxs-lookup"><span data-stu-id="da147-242">Key</span></span>|<span data-ttu-id="da147-243">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-243">Value Type</span></span>|<span data-ttu-id="da147-244">必要</span><span class="sxs-lookup"><span data-stu-id="da147-244">Required</span></span>|<span data-ttu-id="da147-245">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-245">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-246">operation</span><span class="sxs-lookup"><span data-stu-id="da147-246">operation</span></span>|<span data-ttu-id="da147-247">字串</span><span class="sxs-lookup"><span data-stu-id="da147-247">string</span></span>|<span data-ttu-id="da147-248">是</span><span class="sxs-lookup"><span data-stu-id="da147-248">Yes</span></span>|`com.microsoft:schedule-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-249">uint</span><span class="sxs-lookup"><span data-stu-id="da147-249">uint</span></span>|<span data-ttu-id="da147-250">否</span><span class="sxs-lookup"><span data-stu-id="da147-250">No</span></span>|<span data-ttu-id="da147-251">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-251">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-252">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-252">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-253">Key</span><span class="sxs-lookup"><span data-stu-id="da147-253">Key</span></span>|<span data-ttu-id="da147-254">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-254">Value Type</span></span>|<span data-ttu-id="da147-255">必要</span><span class="sxs-lookup"><span data-stu-id="da147-255">Required</span></span>|<span data-ttu-id="da147-256">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-256">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-257">上限</span><span class="sxs-lookup"><span data-stu-id="da147-257">messages</span></span>|<span data-ttu-id="da147-258">對應的清單</span><span class="sxs-lookup"><span data-stu-id="da147-258">list of maps</span></span>|<span data-ttu-id="da147-259">是</span><span class="sxs-lookup"><span data-stu-id="da147-259">Yes</span></span>|<span data-ttu-id="da147-260">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="da147-260">List of messages in which every map represents a message.</span></span>|  
  
<span data-ttu-id="da147-261">hello 對應表示訊息必須包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-261">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="da147-262">Key</span><span class="sxs-lookup"><span data-stu-id="da147-262">Key</span></span>|<span data-ttu-id="da147-263">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-263">Value Type</span></span>|<span data-ttu-id="da147-264">必要</span><span class="sxs-lookup"><span data-stu-id="da147-264">Required</span></span>|<span data-ttu-id="da147-265">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-265">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-266">message-id</span><span class="sxs-lookup"><span data-stu-id="da147-266">message-id</span></span>|<span data-ttu-id="da147-267">字串</span><span class="sxs-lookup"><span data-stu-id="da147-267">string</span></span>|<span data-ttu-id="da147-268">是</span><span class="sxs-lookup"><span data-stu-id="da147-268">Yes</span></span>|<span data-ttu-id="da147-269">`amqpMessage.Properties.MessageId` 為字串</span><span class="sxs-lookup"><span data-stu-id="da147-269">`amqpMessage.Properties.MessageId` as string</span></span>|  
|<span data-ttu-id="da147-270">session-id</span><span class="sxs-lookup"><span data-stu-id="da147-270">session-id</span></span>|<span data-ttu-id="da147-271">string</span><span class="sxs-lookup"><span data-stu-id="da147-271">string</span></span>|<span data-ttu-id="da147-272">是</span><span class="sxs-lookup"><span data-stu-id="da147-272">Yes</span></span>|`amqpMessage.Properties.GroupId as string`|  
|<span data-ttu-id="da147-273">partition-key</span><span class="sxs-lookup"><span data-stu-id="da147-273">partition-key</span></span>|<span data-ttu-id="da147-274">字串</span><span class="sxs-lookup"><span data-stu-id="da147-274">string</span></span>|<span data-ttu-id="da147-275">是</span><span class="sxs-lookup"><span data-stu-id="da147-275">Yes</span></span>|`amqpMessage.MessageAnnotations.”x-opt-partition-key"`|  
|<span data-ttu-id="da147-276">訊息</span><span class="sxs-lookup"><span data-stu-id="da147-276">message</span></span>|<span data-ttu-id="da147-277">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-277">array of byte</span></span>|<span data-ttu-id="da147-278">是</span><span class="sxs-lookup"><span data-stu-id="da147-278">Yes</span></span>|<span data-ttu-id="da147-279">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-279">AMQP 1.0 wire-encoded message.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-280">Response</span><span class="sxs-lookup"><span data-stu-id="da147-280">Response</span></span>  

<span data-ttu-id="da147-281">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-281">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-282">Key</span><span class="sxs-lookup"><span data-stu-id="da147-282">Key</span></span>|<span data-ttu-id="da147-283">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-283">Value Type</span></span>|<span data-ttu-id="da147-284">必要</span><span class="sxs-lookup"><span data-stu-id="da147-284">Required</span></span>|<span data-ttu-id="da147-285">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-285">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-286">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-286">statusCode</span></span>|<span data-ttu-id="da147-287">int</span><span class="sxs-lookup"><span data-stu-id="da147-287">int</span></span>|<span data-ttu-id="da147-288">是</span><span class="sxs-lookup"><span data-stu-id="da147-288">Yes</span></span>|<span data-ttu-id="da147-289">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-289">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-290">200：確定 – 成功，否則失敗。</span><span class="sxs-lookup"><span data-stu-id="da147-290">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="da147-291">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-291">statusDescription</span></span>|<span data-ttu-id="da147-292">字串</span><span class="sxs-lookup"><span data-stu-id="da147-292">string</span></span>|<span data-ttu-id="da147-293">否</span><span class="sxs-lookup"><span data-stu-id="da147-293">No</span></span>|<span data-ttu-id="da147-294">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-294">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-295">hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：</span><span class="sxs-lookup"><span data-stu-id="da147-295">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-296">Key</span><span class="sxs-lookup"><span data-stu-id="da147-296">Key</span></span>|<span data-ttu-id="da147-297">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-297">Value Type</span></span>|<span data-ttu-id="da147-298">必要</span><span class="sxs-lookup"><span data-stu-id="da147-298">Required</span></span>|<span data-ttu-id="da147-299">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-299">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-300">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="da147-300">sequence-numbers</span></span>|<span data-ttu-id="da147-301">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-301">array of long</span></span>|<span data-ttu-id="da147-302">是</span><span class="sxs-lookup"><span data-stu-id="da147-302">Yes</span></span>|<span data-ttu-id="da147-303">排定訊息的序號。</span><span class="sxs-lookup"><span data-stu-id="da147-303">Sequence number of scheduled messages.</span></span> <span data-ttu-id="da147-304">序號是使用的 toocancel。</span><span class="sxs-lookup"><span data-stu-id="da147-304">Sequence number is used toocancel.</span></span>|  
  
### <a name="cancel-scheduled-message"></a><span data-ttu-id="da147-305">取消排定的訊息</span><span class="sxs-lookup"><span data-stu-id="da147-305">Cancel Scheduled Message</span></span>  

<span data-ttu-id="da147-306">取消排定的訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-306">Cancels scheduled messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-307">要求</span><span class="sxs-lookup"><span data-stu-id="da147-307">Request</span></span>  

<span data-ttu-id="da147-308">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-308">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-309">Key</span><span class="sxs-lookup"><span data-stu-id="da147-309">Key</span></span>|<span data-ttu-id="da147-310">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-310">Value Type</span></span>|<span data-ttu-id="da147-311">必要</span><span class="sxs-lookup"><span data-stu-id="da147-311">Required</span></span>|<span data-ttu-id="da147-312">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-312">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-313">operation</span><span class="sxs-lookup"><span data-stu-id="da147-313">operation</span></span>|<span data-ttu-id="da147-314">字串</span><span class="sxs-lookup"><span data-stu-id="da147-314">string</span></span>|<span data-ttu-id="da147-315">是</span><span class="sxs-lookup"><span data-stu-id="da147-315">Yes</span></span>|`com.microsoft:cancel-scheduled-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-316">uint</span><span class="sxs-lookup"><span data-stu-id="da147-316">uint</span></span>|<span data-ttu-id="da147-317">否</span><span class="sxs-lookup"><span data-stu-id="da147-317">No</span></span>|<span data-ttu-id="da147-318">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-318">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-319">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-319">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-320">Key</span><span class="sxs-lookup"><span data-stu-id="da147-320">Key</span></span>|<span data-ttu-id="da147-321">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-321">Value Type</span></span>|<span data-ttu-id="da147-322">必要</span><span class="sxs-lookup"><span data-stu-id="da147-322">Required</span></span>|<span data-ttu-id="da147-323">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-323">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-324">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="da147-324">sequence-numbers</span></span>|<span data-ttu-id="da147-325">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-325">array of long</span></span>|<span data-ttu-id="da147-326">是</span><span class="sxs-lookup"><span data-stu-id="da147-326">Yes</span></span>|<span data-ttu-id="da147-327">排定的訊息 toocancel 順序編號。</span><span class="sxs-lookup"><span data-stu-id="da147-327">Sequence numbers of scheduled messages toocancel.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-328">Response</span><span class="sxs-lookup"><span data-stu-id="da147-328">Response</span></span>  

<span data-ttu-id="da147-329">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-329">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-330">Key</span><span class="sxs-lookup"><span data-stu-id="da147-330">Key</span></span>|<span data-ttu-id="da147-331">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-331">Value Type</span></span>|<span data-ttu-id="da147-332">必要</span><span class="sxs-lookup"><span data-stu-id="da147-332">Required</span></span>|<span data-ttu-id="da147-333">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-333">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-334">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-334">statusCode</span></span>|<span data-ttu-id="da147-335">int</span><span class="sxs-lookup"><span data-stu-id="da147-335">int</span></span>|<span data-ttu-id="da147-336">是</span><span class="sxs-lookup"><span data-stu-id="da147-336">Yes</span></span>|<span data-ttu-id="da147-337">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-337">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-338">200：確定 – 成功，否則失敗。</span><span class="sxs-lookup"><span data-stu-id="da147-338">200: OK – success, otherwise failed.</span></span>|  
|<span data-ttu-id="da147-339">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-339">statusDescription</span></span>|<span data-ttu-id="da147-340">字串</span><span class="sxs-lookup"><span data-stu-id="da147-340">string</span></span>|<span data-ttu-id="da147-341">否</span><span class="sxs-lookup"><span data-stu-id="da147-341">No</span></span>|<span data-ttu-id="da147-342">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-342">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-343">hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：</span><span class="sxs-lookup"><span data-stu-id="da147-343">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-344">Key</span><span class="sxs-lookup"><span data-stu-id="da147-344">Key</span></span>|<span data-ttu-id="da147-345">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-345">Value Type</span></span>|<span data-ttu-id="da147-346">必要</span><span class="sxs-lookup"><span data-stu-id="da147-346">Required</span></span>|<span data-ttu-id="da147-347">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-347">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-348">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="da147-348">sequence-numbers</span></span>|<span data-ttu-id="da147-349">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-349">array of long</span></span>|<span data-ttu-id="da147-350">是</span><span class="sxs-lookup"><span data-stu-id="da147-350">Yes</span></span>|<span data-ttu-id="da147-351">排定訊息的序號。</span><span class="sxs-lookup"><span data-stu-id="da147-351">Sequence number of scheduled messages.</span></span> <span data-ttu-id="da147-352">序號是使用的 toocancel。</span><span class="sxs-lookup"><span data-stu-id="da147-352">Sequence number is used toocancel.</span></span>|  
  
## <a name="session-operations"></a><span data-ttu-id="da147-353">工作階段作業</span><span class="sxs-lookup"><span data-stu-id="da147-353">Session Operations</span></span>  
  
### <a name="session-renew-lock"></a><span data-ttu-id="da147-354">工作階段更新鎖定</span><span class="sxs-lookup"><span data-stu-id="da147-354">Session Renew Lock</span></span>  

<span data-ttu-id="da147-355">延伸 hello 鎖定訊息的 hello hello 實體描述中指定的時間。</span><span class="sxs-lookup"><span data-stu-id="da147-355">Extends hello lock of a message by hello time specified in hello entity description.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-356">要求</span><span class="sxs-lookup"><span data-stu-id="da147-356">Request</span></span>  

<span data-ttu-id="da147-357">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-357">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-358">Key</span><span class="sxs-lookup"><span data-stu-id="da147-358">Key</span></span>|<span data-ttu-id="da147-359">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-359">Value Type</span></span>|<span data-ttu-id="da147-360">必要</span><span class="sxs-lookup"><span data-stu-id="da147-360">Required</span></span>|<span data-ttu-id="da147-361">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-361">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-362">operation</span><span class="sxs-lookup"><span data-stu-id="da147-362">operation</span></span>|<span data-ttu-id="da147-363">字串</span><span class="sxs-lookup"><span data-stu-id="da147-363">string</span></span>|<span data-ttu-id="da147-364">是</span><span class="sxs-lookup"><span data-stu-id="da147-364">Yes</span></span>|`com.microsoft:renew-session-lock`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-365">uint</span><span class="sxs-lookup"><span data-stu-id="da147-365">uint</span></span>|<span data-ttu-id="da147-366">否</span><span class="sxs-lookup"><span data-stu-id="da147-366">No</span></span>|<span data-ttu-id="da147-367">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-367">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-368">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-368">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-369">Key</span><span class="sxs-lookup"><span data-stu-id="da147-369">Key</span></span>|<span data-ttu-id="da147-370">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-370">Value Type</span></span>|<span data-ttu-id="da147-371">必要</span><span class="sxs-lookup"><span data-stu-id="da147-371">Required</span></span>|<span data-ttu-id="da147-372">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-372">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-373">session-id</span><span class="sxs-lookup"><span data-stu-id="da147-373">session-id</span></span>|<span data-ttu-id="da147-374">string</span><span class="sxs-lookup"><span data-stu-id="da147-374">string</span></span>|<span data-ttu-id="da147-375">是</span><span class="sxs-lookup"><span data-stu-id="da147-375">Yes</span></span>|<span data-ttu-id="da147-376">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="da147-376">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-377">Response</span><span class="sxs-lookup"><span data-stu-id="da147-377">Response</span></span>  

<span data-ttu-id="da147-378">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-378">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-379">Key</span><span class="sxs-lookup"><span data-stu-id="da147-379">Key</span></span>|<span data-ttu-id="da147-380">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-380">Value Type</span></span>|<span data-ttu-id="da147-381">必要</span><span class="sxs-lookup"><span data-stu-id="da147-381">Required</span></span>|<span data-ttu-id="da147-382">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-382">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-383">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-383">statusCode</span></span>|<span data-ttu-id="da147-384">int</span><span class="sxs-lookup"><span data-stu-id="da147-384">int</span></span>|<span data-ttu-id="da147-385">是</span><span class="sxs-lookup"><span data-stu-id="da147-385">Yes</span></span>|<span data-ttu-id="da147-386">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-386">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-387">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="da147-387">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="da147-388">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="da147-388">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="da147-389">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-389">statusDescription</span></span>|<span data-ttu-id="da147-390">字串</span><span class="sxs-lookup"><span data-stu-id="da147-390">string</span></span>|<span data-ttu-id="da147-391">否</span><span class="sxs-lookup"><span data-stu-id="da147-391">No</span></span>|<span data-ttu-id="da147-392">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-392">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-393">hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：</span><span class="sxs-lookup"><span data-stu-id="da147-393">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-394">Key</span><span class="sxs-lookup"><span data-stu-id="da147-394">Key</span></span>|<span data-ttu-id="da147-395">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-395">Value Type</span></span>|<span data-ttu-id="da147-396">必要</span><span class="sxs-lookup"><span data-stu-id="da147-396">Required</span></span>|<span data-ttu-id="da147-397">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-397">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-398">expiration</span><span class="sxs-lookup"><span data-stu-id="da147-398">expiration</span></span>|<span data-ttu-id="da147-399">timestamp</span><span class="sxs-lookup"><span data-stu-id="da147-399">timestamp</span></span>|<span data-ttu-id="da147-400">是</span><span class="sxs-lookup"><span data-stu-id="da147-400">Yes</span></span>|<span data-ttu-id="da147-401">新的到期日。</span><span class="sxs-lookup"><span data-stu-id="da147-401">New expiration.</span></span>|  
  
### <a name="peek-session-message"></a><span data-ttu-id="da147-402">查看工作階段訊息</span><span class="sxs-lookup"><span data-stu-id="da147-402">Peek Session Message</span></span>  

<span data-ttu-id="da147-403">查看工作階段訊息而不用鎖定。</span><span class="sxs-lookup"><span data-stu-id="da147-403">Peeks session messages without locking.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-404">要求</span><span class="sxs-lookup"><span data-stu-id="da147-404">Request</span></span>  

<span data-ttu-id="da147-405">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-405">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-406">Key</span><span class="sxs-lookup"><span data-stu-id="da147-406">Key</span></span>|<span data-ttu-id="da147-407">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-407">Value Type</span></span>|<span data-ttu-id="da147-408">必要</span><span class="sxs-lookup"><span data-stu-id="da147-408">Required</span></span>|<span data-ttu-id="da147-409">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-409">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-410">operation</span><span class="sxs-lookup"><span data-stu-id="da147-410">operation</span></span>|<span data-ttu-id="da147-411">字串</span><span class="sxs-lookup"><span data-stu-id="da147-411">string</span></span>|<span data-ttu-id="da147-412">是</span><span class="sxs-lookup"><span data-stu-id="da147-412">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-413">uint</span><span class="sxs-lookup"><span data-stu-id="da147-413">uint</span></span>|<span data-ttu-id="da147-414">否</span><span class="sxs-lookup"><span data-stu-id="da147-414">No</span></span>|<span data-ttu-id="da147-415">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-415">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-416">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-416">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-417">Key</span><span class="sxs-lookup"><span data-stu-id="da147-417">Key</span></span>|<span data-ttu-id="da147-418">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-418">Value Type</span></span>|<span data-ttu-id="da147-419">必要</span><span class="sxs-lookup"><span data-stu-id="da147-419">Required</span></span>|<span data-ttu-id="da147-420">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-420">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-421">from-sequence-number</span><span class="sxs-lookup"><span data-stu-id="da147-421">from-sequence-number</span></span>|<span data-ttu-id="da147-422">long</span><span class="sxs-lookup"><span data-stu-id="da147-422">long</span></span>|<span data-ttu-id="da147-423">是</span><span class="sxs-lookup"><span data-stu-id="da147-423">Yes</span></span>|<span data-ttu-id="da147-424">從哪些 toostart 查看的序號。</span><span class="sxs-lookup"><span data-stu-id="da147-424">Sequence number from which toostart peek.</span></span>|  
|<span data-ttu-id="da147-425">message-count</span><span class="sxs-lookup"><span data-stu-id="da147-425">message-count</span></span>|<span data-ttu-id="da147-426">int</span><span class="sxs-lookup"><span data-stu-id="da147-426">int</span></span>|<span data-ttu-id="da147-427">是</span><span class="sxs-lookup"><span data-stu-id="da147-427">Yes</span></span>|<span data-ttu-id="da147-428">訊息 toopeek 的數目上限。</span><span class="sxs-lookup"><span data-stu-id="da147-428">Maximum number of messages toopeek.</span></span>|  
|<span data-ttu-id="da147-429">session-id</span><span class="sxs-lookup"><span data-stu-id="da147-429">session-id</span></span>|<span data-ttu-id="da147-430">string</span><span class="sxs-lookup"><span data-stu-id="da147-430">string</span></span>|<span data-ttu-id="da147-431">是</span><span class="sxs-lookup"><span data-stu-id="da147-431">Yes</span></span>|<span data-ttu-id="da147-432">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="da147-432">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-433">Response</span><span class="sxs-lookup"><span data-stu-id="da147-433">Response</span></span>  

<span data-ttu-id="da147-434">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-434">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-435">Key</span><span class="sxs-lookup"><span data-stu-id="da147-435">Key</span></span>|<span data-ttu-id="da147-436">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-436">Value Type</span></span>|<span data-ttu-id="da147-437">必要</span><span class="sxs-lookup"><span data-stu-id="da147-437">Required</span></span>|<span data-ttu-id="da147-438">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-438">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-439">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-439">statusCode</span></span>|<span data-ttu-id="da147-440">int</span><span class="sxs-lookup"><span data-stu-id="da147-440">int</span></span>|<span data-ttu-id="da147-441">是</span><span class="sxs-lookup"><span data-stu-id="da147-441">Yes</span></span>|<span data-ttu-id="da147-442">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-442">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-443">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="da147-443">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="da147-444">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="da147-444">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="da147-445">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-445">statusDescription</span></span>|<span data-ttu-id="da147-446">字串</span><span class="sxs-lookup"><span data-stu-id="da147-446">string</span></span>|<span data-ttu-id="da147-447">否</span><span class="sxs-lookup"><span data-stu-id="da147-447">No</span></span>|<span data-ttu-id="da147-448">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-448">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-449">hello 回應訊息內文必須包含**amqp 值**hello 下列項目與包含對應區段：</span><span class="sxs-lookup"><span data-stu-id="da147-449">hello response message body must consist of an **amqp-value** section containing a map with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-450">Key</span><span class="sxs-lookup"><span data-stu-id="da147-450">Key</span></span>|<span data-ttu-id="da147-451">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-451">Value Type</span></span>|<span data-ttu-id="da147-452">必要</span><span class="sxs-lookup"><span data-stu-id="da147-452">Required</span></span>|<span data-ttu-id="da147-453">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-453">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-454">上限</span><span class="sxs-lookup"><span data-stu-id="da147-454">messages</span></span>|<span data-ttu-id="da147-455">對應的清單</span><span class="sxs-lookup"><span data-stu-id="da147-455">list of maps</span></span>|<span data-ttu-id="da147-456">是</span><span class="sxs-lookup"><span data-stu-id="da147-456">Yes</span></span>|<span data-ttu-id="da147-457">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="da147-457">List of messages in which every map represents a message.</span></span>|  
  
 <span data-ttu-id="da147-458">hello 對應表示訊息必須包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-458">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="da147-459">Key</span><span class="sxs-lookup"><span data-stu-id="da147-459">Key</span></span>|<span data-ttu-id="da147-460">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-460">Value Type</span></span>|<span data-ttu-id="da147-461">必要</span><span class="sxs-lookup"><span data-stu-id="da147-461">Required</span></span>|<span data-ttu-id="da147-462">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-462">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-463">訊息</span><span class="sxs-lookup"><span data-stu-id="da147-463">message</span></span>|<span data-ttu-id="da147-464">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-464">array of byte</span></span>|<span data-ttu-id="da147-465">是</span><span class="sxs-lookup"><span data-stu-id="da147-465">Yes</span></span>|<span data-ttu-id="da147-466">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-466">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="set-session-state"></a><span data-ttu-id="da147-467">設定工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="da147-467">Set Session State</span></span>  

<span data-ttu-id="da147-468">設定 hello 工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="da147-468">Sets hello state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-469">要求</span><span class="sxs-lookup"><span data-stu-id="da147-469">Request</span></span>  

<span data-ttu-id="da147-470">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-470">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-471">Key</span><span class="sxs-lookup"><span data-stu-id="da147-471">Key</span></span>|<span data-ttu-id="da147-472">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-472">Value Type</span></span>|<span data-ttu-id="da147-473">必要</span><span class="sxs-lookup"><span data-stu-id="da147-473">Required</span></span>|<span data-ttu-id="da147-474">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-474">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-475">operation</span><span class="sxs-lookup"><span data-stu-id="da147-475">operation</span></span>|<span data-ttu-id="da147-476">字串</span><span class="sxs-lookup"><span data-stu-id="da147-476">string</span></span>|<span data-ttu-id="da147-477">是</span><span class="sxs-lookup"><span data-stu-id="da147-477">Yes</span></span>|`com.microsoft:peek-message`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-478">uint</span><span class="sxs-lookup"><span data-stu-id="da147-478">uint</span></span>|<span data-ttu-id="da147-479">否</span><span class="sxs-lookup"><span data-stu-id="da147-479">No</span></span>|<span data-ttu-id="da147-480">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-480">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-481">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-481">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-482">Key</span><span class="sxs-lookup"><span data-stu-id="da147-482">Key</span></span>|<span data-ttu-id="da147-483">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-483">Value Type</span></span>|<span data-ttu-id="da147-484">必要</span><span class="sxs-lookup"><span data-stu-id="da147-484">Required</span></span>|<span data-ttu-id="da147-485">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-485">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-486">session-id</span><span class="sxs-lookup"><span data-stu-id="da147-486">session-id</span></span>|<span data-ttu-id="da147-487">string</span><span class="sxs-lookup"><span data-stu-id="da147-487">string</span></span>|<span data-ttu-id="da147-488">是</span><span class="sxs-lookup"><span data-stu-id="da147-488">Yes</span></span>|<span data-ttu-id="da147-489">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="da147-489">Session ID.</span></span>|  
|<span data-ttu-id="da147-490">session-state</span><span class="sxs-lookup"><span data-stu-id="da147-490">session-state</span></span>|<span data-ttu-id="da147-491">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-491">array of bytes</span></span>|<span data-ttu-id="da147-492">是</span><span class="sxs-lookup"><span data-stu-id="da147-492">Yes</span></span>|<span data-ttu-id="da147-493">不透明的二進位資料。</span><span class="sxs-lookup"><span data-stu-id="da147-493">Opaque binary data.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-494">Response</span><span class="sxs-lookup"><span data-stu-id="da147-494">Response</span></span>  

<span data-ttu-id="da147-495">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-495">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-496">Key</span><span class="sxs-lookup"><span data-stu-id="da147-496">Key</span></span>|<span data-ttu-id="da147-497">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-497">Value Type</span></span>|<span data-ttu-id="da147-498">必要</span><span class="sxs-lookup"><span data-stu-id="da147-498">Required</span></span>|<span data-ttu-id="da147-499">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-499">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-500">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-500">statusCode</span></span>|<span data-ttu-id="da147-501">int</span><span class="sxs-lookup"><span data-stu-id="da147-501">int</span></span>|<span data-ttu-id="da147-502">是</span><span class="sxs-lookup"><span data-stu-id="da147-502">Yes</span></span>|<span data-ttu-id="da147-503">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-503">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-504">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="da147-504">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="da147-505">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-505">statusDescription</span></span>|<span data-ttu-id="da147-506">字串</span><span class="sxs-lookup"><span data-stu-id="da147-506">string</span></span>|<span data-ttu-id="da147-507">否</span><span class="sxs-lookup"><span data-stu-id="da147-507">No</span></span>|<span data-ttu-id="da147-508">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-508">Description of hello status.</span></span>|  
  
### <a name="get-session-state"></a><span data-ttu-id="da147-509">取得工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="da147-509">Get Session State</span></span>  

<span data-ttu-id="da147-510">取得工作階段的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="da147-510">Gets hello state of a session.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-511">要求</span><span class="sxs-lookup"><span data-stu-id="da147-511">Request</span></span>  

<span data-ttu-id="da147-512">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-512">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-513">Key</span><span class="sxs-lookup"><span data-stu-id="da147-513">Key</span></span>|<span data-ttu-id="da147-514">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-514">Value Type</span></span>|<span data-ttu-id="da147-515">必要</span><span class="sxs-lookup"><span data-stu-id="da147-515">Required</span></span>|<span data-ttu-id="da147-516">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-516">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-517">operation</span><span class="sxs-lookup"><span data-stu-id="da147-517">operation</span></span>|<span data-ttu-id="da147-518">字串</span><span class="sxs-lookup"><span data-stu-id="da147-518">string</span></span>|<span data-ttu-id="da147-519">是</span><span class="sxs-lookup"><span data-stu-id="da147-519">Yes</span></span>|`com.microsoft:get-session-state`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-520">uint</span><span class="sxs-lookup"><span data-stu-id="da147-520">uint</span></span>|<span data-ttu-id="da147-521">否</span><span class="sxs-lookup"><span data-stu-id="da147-521">No</span></span>|<span data-ttu-id="da147-522">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-522">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-523">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-523">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-524">Key</span><span class="sxs-lookup"><span data-stu-id="da147-524">Key</span></span>|<span data-ttu-id="da147-525">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-525">Value Type</span></span>|<span data-ttu-id="da147-526">必要</span><span class="sxs-lookup"><span data-stu-id="da147-526">Required</span></span>|<span data-ttu-id="da147-527">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-527">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-528">session-id</span><span class="sxs-lookup"><span data-stu-id="da147-528">session-id</span></span>|<span data-ttu-id="da147-529">string</span><span class="sxs-lookup"><span data-stu-id="da147-529">string</span></span>|<span data-ttu-id="da147-530">是</span><span class="sxs-lookup"><span data-stu-id="da147-530">Yes</span></span>|<span data-ttu-id="da147-531">工作階段識別碼。</span><span class="sxs-lookup"><span data-stu-id="da147-531">Session ID.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-532">Response</span><span class="sxs-lookup"><span data-stu-id="da147-532">Response</span></span>  

<span data-ttu-id="da147-533">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-533">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-534">Key</span><span class="sxs-lookup"><span data-stu-id="da147-534">Key</span></span>|<span data-ttu-id="da147-535">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-535">Value Type</span></span>|<span data-ttu-id="da147-536">必要</span><span class="sxs-lookup"><span data-stu-id="da147-536">Required</span></span>|<span data-ttu-id="da147-537">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-537">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-538">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-538">statusCode</span></span>|<span data-ttu-id="da147-539">int</span><span class="sxs-lookup"><span data-stu-id="da147-539">int</span></span>|<span data-ttu-id="da147-540">是</span><span class="sxs-lookup"><span data-stu-id="da147-540">Yes</span></span>|<span data-ttu-id="da147-541">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-541">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-542">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="da147-542">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="da147-543">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-543">statusDescription</span></span>|<span data-ttu-id="da147-544">字串</span><span class="sxs-lookup"><span data-stu-id="da147-544">string</span></span>|<span data-ttu-id="da147-545">否</span><span class="sxs-lookup"><span data-stu-id="da147-545">No</span></span>|<span data-ttu-id="da147-546">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-546">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-547">hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-547">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-548">Key</span><span class="sxs-lookup"><span data-stu-id="da147-548">Key</span></span>|<span data-ttu-id="da147-549">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-549">Value Type</span></span>|<span data-ttu-id="da147-550">必要</span><span class="sxs-lookup"><span data-stu-id="da147-550">Required</span></span>|<span data-ttu-id="da147-551">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-551">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-552">session-state</span><span class="sxs-lookup"><span data-stu-id="da147-552">session-state</span></span>|<span data-ttu-id="da147-553">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-553">array of bytes</span></span>|<span data-ttu-id="da147-554">是</span><span class="sxs-lookup"><span data-stu-id="da147-554">Yes</span></span>|<span data-ttu-id="da147-555">不透明的二進位資料。</span><span class="sxs-lookup"><span data-stu-id="da147-555">Opaque binary data.</span></span>|  
  
### <a name="enumerate-sessions"></a><span data-ttu-id="da147-556">列舉工作階段</span><span class="sxs-lookup"><span data-stu-id="da147-556">Enumerate Sessions</span></span>  

<span data-ttu-id="da147-557">列舉訊息實體上的工作階段。</span><span class="sxs-lookup"><span data-stu-id="da147-557">Enumerates sessions on a messaging entity.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-558">要求</span><span class="sxs-lookup"><span data-stu-id="da147-558">Request</span></span>  

<span data-ttu-id="da147-559">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-559">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-560">Key</span><span class="sxs-lookup"><span data-stu-id="da147-560">Key</span></span>|<span data-ttu-id="da147-561">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-561">Value Type</span></span>|<span data-ttu-id="da147-562">必要</span><span class="sxs-lookup"><span data-stu-id="da147-562">Required</span></span>|<span data-ttu-id="da147-563">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-563">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-564">operation</span><span class="sxs-lookup"><span data-stu-id="da147-564">operation</span></span>|<span data-ttu-id="da147-565">字串</span><span class="sxs-lookup"><span data-stu-id="da147-565">string</span></span>|<span data-ttu-id="da147-566">是</span><span class="sxs-lookup"><span data-stu-id="da147-566">Yes</span></span>|`com.microsoft:get-message-sessions`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-567">uint</span><span class="sxs-lookup"><span data-stu-id="da147-567">uint</span></span>|<span data-ttu-id="da147-568">否</span><span class="sxs-lookup"><span data-stu-id="da147-568">No</span></span>|<span data-ttu-id="da147-569">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-569">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-570">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-570">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-571">Key</span><span class="sxs-lookup"><span data-stu-id="da147-571">Key</span></span>|<span data-ttu-id="da147-572">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-572">Value Type</span></span>|<span data-ttu-id="da147-573">必要</span><span class="sxs-lookup"><span data-stu-id="da147-573">Required</span></span>|<span data-ttu-id="da147-574">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-574">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-575">last-updated-time</span><span class="sxs-lookup"><span data-stu-id="da147-575">last-updated-time</span></span>|<span data-ttu-id="da147-576">timestamp</span><span class="sxs-lookup"><span data-stu-id="da147-576">timestamp</span></span>|<span data-ttu-id="da147-577">是</span><span class="sxs-lookup"><span data-stu-id="da147-577">Yes</span></span>|<span data-ttu-id="da147-578">篩選 tooinclude 唯一工作階段指定的時間之後更新。</span><span class="sxs-lookup"><span data-stu-id="da147-578">Filter tooinclude only sessions updated after a given time.</span></span>|  
|<span data-ttu-id="da147-579">skip</span><span class="sxs-lookup"><span data-stu-id="da147-579">skip</span></span>|<span data-ttu-id="da147-580">int</span><span class="sxs-lookup"><span data-stu-id="da147-580">int</span></span>|<span data-ttu-id="da147-581">是</span><span class="sxs-lookup"><span data-stu-id="da147-581">Yes</span></span>|<span data-ttu-id="da147-582">略過工作階段數。</span><span class="sxs-lookup"><span data-stu-id="da147-582">Skip a number of sessions.</span></span>|  
|<span data-ttu-id="da147-583">top</span><span class="sxs-lookup"><span data-stu-id="da147-583">top</span></span>|<span data-ttu-id="da147-584">int</span><span class="sxs-lookup"><span data-stu-id="da147-584">int</span></span>|<span data-ttu-id="da147-585">是</span><span class="sxs-lookup"><span data-stu-id="da147-585">Yes</span></span>|<span data-ttu-id="da147-586">工作階段數上限。</span><span class="sxs-lookup"><span data-stu-id="da147-586">Maximum number of sessions.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-587">Response</span><span class="sxs-lookup"><span data-stu-id="da147-587">Response</span></span>  

<span data-ttu-id="da147-588">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-588">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-589">Key</span><span class="sxs-lookup"><span data-stu-id="da147-589">Key</span></span>|<span data-ttu-id="da147-590">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-590">Value Type</span></span>|<span data-ttu-id="da147-591">必要</span><span class="sxs-lookup"><span data-stu-id="da147-591">Required</span></span>|<span data-ttu-id="da147-592">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-592">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-593">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-593">statusCode</span></span>|<span data-ttu-id="da147-594">int</span><span class="sxs-lookup"><span data-stu-id="da147-594">int</span></span>|<span data-ttu-id="da147-595">是</span><span class="sxs-lookup"><span data-stu-id="da147-595">Yes</span></span>|<span data-ttu-id="da147-596">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-596">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-597">200：確定 – 有多個訊息</span><span class="sxs-lookup"><span data-stu-id="da147-597">200: OK – has more messages</span></span><br /><br /> <span data-ttu-id="da147-598">0xcc︰沒有內容 – 沒有其他訊息</span><span class="sxs-lookup"><span data-stu-id="da147-598">0xcc: No content – no more messages</span></span>|  
|<span data-ttu-id="da147-599">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-599">statusDescription</span></span>|<span data-ttu-id="da147-600">字串</span><span class="sxs-lookup"><span data-stu-id="da147-600">string</span></span>|<span data-ttu-id="da147-601">否</span><span class="sxs-lookup"><span data-stu-id="da147-601">No</span></span>|<span data-ttu-id="da147-602">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-602">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-603">hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-603">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-604">Key</span><span class="sxs-lookup"><span data-stu-id="da147-604">Key</span></span>|<span data-ttu-id="da147-605">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-605">Value Type</span></span>|<span data-ttu-id="da147-606">必要</span><span class="sxs-lookup"><span data-stu-id="da147-606">Required</span></span>|<span data-ttu-id="da147-607">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-607">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-608">skip</span><span class="sxs-lookup"><span data-stu-id="da147-608">skip</span></span>|<span data-ttu-id="da147-609">int</span><span class="sxs-lookup"><span data-stu-id="da147-609">int</span></span>|<span data-ttu-id="da147-610">是</span><span class="sxs-lookup"><span data-stu-id="da147-610">Yes</span></span>|<span data-ttu-id="da147-611">如果狀態碼為 200 所略過的工作階段數。</span><span class="sxs-lookup"><span data-stu-id="da147-611">Number of skipped sessions if status code is 200.</span></span>|  
|<span data-ttu-id="da147-612">sessions-ids</span><span class="sxs-lookup"><span data-stu-id="da147-612">sessions-ids</span></span>|<span data-ttu-id="da147-613">字串的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-613">array of strings</span></span>|<span data-ttu-id="da147-614">是</span><span class="sxs-lookup"><span data-stu-id="da147-614">Yes</span></span>|<span data-ttu-id="da147-615">如果狀態碼為 200 的工作階段識別碼陣列。</span><span class="sxs-lookup"><span data-stu-id="da147-615">Array of session IDs if status code is 200.</span></span>|  
  
## <a name="rule-operations"></a><span data-ttu-id="da147-616">規則作業</span><span class="sxs-lookup"><span data-stu-id="da147-616">Rule operations</span></span>  
  
### <a name="add-rule"></a><span data-ttu-id="da147-617">新增規則</span><span class="sxs-lookup"><span data-stu-id="da147-617">Add Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-618">要求</span><span class="sxs-lookup"><span data-stu-id="da147-618">Request</span></span>  

<span data-ttu-id="da147-619">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-619">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-620">Key</span><span class="sxs-lookup"><span data-stu-id="da147-620">Key</span></span>|<span data-ttu-id="da147-621">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-621">Value Type</span></span>|<span data-ttu-id="da147-622">必要</span><span class="sxs-lookup"><span data-stu-id="da147-622">Required</span></span>|<span data-ttu-id="da147-623">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-623">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-624">operation</span><span class="sxs-lookup"><span data-stu-id="da147-624">operation</span></span>|<span data-ttu-id="da147-625">字串</span><span class="sxs-lookup"><span data-stu-id="da147-625">string</span></span>|<span data-ttu-id="da147-626">是</span><span class="sxs-lookup"><span data-stu-id="da147-626">Yes</span></span>|`com.microsoft:add-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-627">uint</span><span class="sxs-lookup"><span data-stu-id="da147-627">uint</span></span>|<span data-ttu-id="da147-628">否</span><span class="sxs-lookup"><span data-stu-id="da147-628">No</span></span>|<span data-ttu-id="da147-629">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-629">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-630">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-630">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-631">Key</span><span class="sxs-lookup"><span data-stu-id="da147-631">Key</span></span>|<span data-ttu-id="da147-632">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-632">Value Type</span></span>|<span data-ttu-id="da147-633">必要</span><span class="sxs-lookup"><span data-stu-id="da147-633">Required</span></span>|<span data-ttu-id="da147-634">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-634">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-635">rule-name</span><span class="sxs-lookup"><span data-stu-id="da147-635">rule-name</span></span>|<span data-ttu-id="da147-636">字串</span><span class="sxs-lookup"><span data-stu-id="da147-636">string</span></span>|<span data-ttu-id="da147-637">是</span><span class="sxs-lookup"><span data-stu-id="da147-637">Yes</span></span>|<span data-ttu-id="da147-638">規則名稱，不包括訂用帳戶和主題名稱。</span><span class="sxs-lookup"><span data-stu-id="da147-638">Rule name, not including subscription and topic names.</span></span>|  
|<span data-ttu-id="da147-639">rule-description</span><span class="sxs-lookup"><span data-stu-id="da147-639">rule-description</span></span>|<span data-ttu-id="da147-640">map</span><span class="sxs-lookup"><span data-stu-id="da147-640">map</span></span>|<span data-ttu-id="da147-641">是</span><span class="sxs-lookup"><span data-stu-id="da147-641">Yes</span></span>|<span data-ttu-id="da147-642">如下一節中指定的規則描述。</span><span class="sxs-lookup"><span data-stu-id="da147-642">Rule description as specified in next section.</span></span>|  
  
<span data-ttu-id="da147-643">hello**規則描述**地圖必須包含下列項目，hello 其中**sql 篩選**和**相互關聯篩選**互斥：</span><span class="sxs-lookup"><span data-stu-id="da147-643">hello **rule-description** map must include hello following entries, where **sql-filter** and **correlation-filter** are mutually exclusive:</span></span>  
  
|<span data-ttu-id="da147-644">Key</span><span class="sxs-lookup"><span data-stu-id="da147-644">Key</span></span>|<span data-ttu-id="da147-645">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-645">Value Type</span></span>|<span data-ttu-id="da147-646">必要</span><span class="sxs-lookup"><span data-stu-id="da147-646">Required</span></span>|<span data-ttu-id="da147-647">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-647">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-648">sql-filter</span><span class="sxs-lookup"><span data-stu-id="da147-648">sql-filter</span></span>|<span data-ttu-id="da147-649">map</span><span class="sxs-lookup"><span data-stu-id="da147-649">map</span></span>|<span data-ttu-id="da147-650">是</span><span class="sxs-lookup"><span data-stu-id="da147-650">Yes</span></span>|<span data-ttu-id="da147-651">`sql-filter`hello 下一節中所指定。</span><span class="sxs-lookup"><span data-stu-id="da147-651">`sql-filter`, as specified in hello next section.</span></span>|  
|<span data-ttu-id="da147-652">correlation-filter</span><span class="sxs-lookup"><span data-stu-id="da147-652">correlation-filter</span></span>|<span data-ttu-id="da147-653">map</span><span class="sxs-lookup"><span data-stu-id="da147-653">map</span></span>|<span data-ttu-id="da147-654">是</span><span class="sxs-lookup"><span data-stu-id="da147-654">Yes</span></span>|<span data-ttu-id="da147-655">`correlation-filter`hello 下一節中所指定。</span><span class="sxs-lookup"><span data-stu-id="da147-655">`correlation-filter`, as specified in hello next section.</span></span>|  
|<span data-ttu-id="da147-656">sql-rule-action</span><span class="sxs-lookup"><span data-stu-id="da147-656">sql-rule-action</span></span>|<span data-ttu-id="da147-657">map</span><span class="sxs-lookup"><span data-stu-id="da147-657">map</span></span>|<span data-ttu-id="da147-658">是</span><span class="sxs-lookup"><span data-stu-id="da147-658">Yes</span></span>|<span data-ttu-id="da147-659">`sql-rule-action`hello 下一節中所指定。</span><span class="sxs-lookup"><span data-stu-id="da147-659">`sql-rule-action`, as specified in hello next section.</span></span>|  
  
<span data-ttu-id="da147-660">hello sql 篩選地圖必須包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-660">hello sql-filter map must include hello following entries:</span></span>  
  
|<span data-ttu-id="da147-661">Key</span><span class="sxs-lookup"><span data-stu-id="da147-661">Key</span></span>|<span data-ttu-id="da147-662">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-662">Value Type</span></span>|<span data-ttu-id="da147-663">必要</span><span class="sxs-lookup"><span data-stu-id="da147-663">Required</span></span>|<span data-ttu-id="da147-664">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-664">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-665">expression</span><span class="sxs-lookup"><span data-stu-id="da147-665">expression</span></span>|<span data-ttu-id="da147-666">字串</span><span class="sxs-lookup"><span data-stu-id="da147-666">string</span></span>|<span data-ttu-id="da147-667">是</span><span class="sxs-lookup"><span data-stu-id="da147-667">Yes</span></span>|<span data-ttu-id="da147-668">Sql 篩選運算式。</span><span class="sxs-lookup"><span data-stu-id="da147-668">Sql filter expression.</span></span>|  
  
<span data-ttu-id="da147-669">hello**相互關聯篩選**地圖必須包含至少其中一個 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-669">hello **correlation-filter** map must include at least one of hello following entries:</span></span>  
  
|<span data-ttu-id="da147-670">Key</span><span class="sxs-lookup"><span data-stu-id="da147-670">Key</span></span>|<span data-ttu-id="da147-671">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-671">Value Type</span></span>|<span data-ttu-id="da147-672">必要</span><span class="sxs-lookup"><span data-stu-id="da147-672">Required</span></span>|<span data-ttu-id="da147-673">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-673">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-674">correlation-id</span><span class="sxs-lookup"><span data-stu-id="da147-674">correlation-id</span></span>|<span data-ttu-id="da147-675">字串</span><span class="sxs-lookup"><span data-stu-id="da147-675">string</span></span>|<span data-ttu-id="da147-676">否</span><span class="sxs-lookup"><span data-stu-id="da147-676">No</span></span>||  
|<span data-ttu-id="da147-677">message-id</span><span class="sxs-lookup"><span data-stu-id="da147-677">message-id</span></span>|<span data-ttu-id="da147-678">字串</span><span class="sxs-lookup"><span data-stu-id="da147-678">string</span></span>|<span data-ttu-id="da147-679">否</span><span class="sxs-lookup"><span data-stu-id="da147-679">No</span></span>||  
|<span data-ttu-id="da147-680">to</span><span class="sxs-lookup"><span data-stu-id="da147-680">to</span></span>|<span data-ttu-id="da147-681">字串</span><span class="sxs-lookup"><span data-stu-id="da147-681">string</span></span>|<span data-ttu-id="da147-682">否</span><span class="sxs-lookup"><span data-stu-id="da147-682">No</span></span>||  
|<span data-ttu-id="da147-683">reply-to</span><span class="sxs-lookup"><span data-stu-id="da147-683">reply-to</span></span>|<span data-ttu-id="da147-684">string</span><span class="sxs-lookup"><span data-stu-id="da147-684">string</span></span>|<span data-ttu-id="da147-685">否</span><span class="sxs-lookup"><span data-stu-id="da147-685">No</span></span>||  
|<span data-ttu-id="da147-686">標籤</span><span class="sxs-lookup"><span data-stu-id="da147-686">label</span></span>|<span data-ttu-id="da147-687">string</span><span class="sxs-lookup"><span data-stu-id="da147-687">string</span></span>|<span data-ttu-id="da147-688">否</span><span class="sxs-lookup"><span data-stu-id="da147-688">No</span></span>||  
|<span data-ttu-id="da147-689">session-id</span><span class="sxs-lookup"><span data-stu-id="da147-689">session-id</span></span>|<span data-ttu-id="da147-690">string</span><span class="sxs-lookup"><span data-stu-id="da147-690">string</span></span>|<span data-ttu-id="da147-691">否</span><span class="sxs-lookup"><span data-stu-id="da147-691">No</span></span>||  
|<span data-ttu-id="da147-692">reply-to-session-id</span><span class="sxs-lookup"><span data-stu-id="da147-692">reply-to-session-id</span></span>|<span data-ttu-id="da147-693">string</span><span class="sxs-lookup"><span data-stu-id="da147-693">string</span></span>|<span data-ttu-id="da147-694">否</span><span class="sxs-lookup"><span data-stu-id="da147-694">No</span></span>||  
|<span data-ttu-id="da147-695">Content-Type</span><span class="sxs-lookup"><span data-stu-id="da147-695">content-type</span></span>|<span data-ttu-id="da147-696">字串</span><span class="sxs-lookup"><span data-stu-id="da147-696">string</span></span>|<span data-ttu-id="da147-697">否</span><span class="sxs-lookup"><span data-stu-id="da147-697">No</span></span>||  
|<span data-ttu-id="da147-698">properties</span><span class="sxs-lookup"><span data-stu-id="da147-698">properties</span></span>|<span data-ttu-id="da147-699">map</span><span class="sxs-lookup"><span data-stu-id="da147-699">map</span></span>|<span data-ttu-id="da147-700">否</span><span class="sxs-lookup"><span data-stu-id="da147-700">No</span></span>|<span data-ttu-id="da147-701">對應 tooService 匯流排[BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties)。</span><span class="sxs-lookup"><span data-stu-id="da147-701">Maps tooService Bus [BrokeredMessage.Properties](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Properties).</span></span>|  
  
<span data-ttu-id="da147-702">hello **sql 規則動作**地圖必須包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-702">hello **sql-rule-action** map must include hello following entries:</span></span>  
  
|<span data-ttu-id="da147-703">Key</span><span class="sxs-lookup"><span data-stu-id="da147-703">Key</span></span>|<span data-ttu-id="da147-704">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-704">Value Type</span></span>|<span data-ttu-id="da147-705">必要</span><span class="sxs-lookup"><span data-stu-id="da147-705">Required</span></span>|<span data-ttu-id="da147-706">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-706">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-707">expression</span><span class="sxs-lookup"><span data-stu-id="da147-707">expression</span></span>|<span data-ttu-id="da147-708">字串</span><span class="sxs-lookup"><span data-stu-id="da147-708">string</span></span>|<span data-ttu-id="da147-709">是</span><span class="sxs-lookup"><span data-stu-id="da147-709">Yes</span></span>|<span data-ttu-id="da147-710">Sql 動作運算式。</span><span class="sxs-lookup"><span data-stu-id="da147-710">Sql action expression.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-711">Response</span><span class="sxs-lookup"><span data-stu-id="da147-711">Response</span></span>  

<span data-ttu-id="da147-712">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-712">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-713">Key</span><span class="sxs-lookup"><span data-stu-id="da147-713">Key</span></span>|<span data-ttu-id="da147-714">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-714">Value Type</span></span>|<span data-ttu-id="da147-715">必要</span><span class="sxs-lookup"><span data-stu-id="da147-715">Required</span></span>|<span data-ttu-id="da147-716">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-716">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-717">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-717">statusCode</span></span>|<span data-ttu-id="da147-718">int</span><span class="sxs-lookup"><span data-stu-id="da147-718">int</span></span>|<span data-ttu-id="da147-719">是</span><span class="sxs-lookup"><span data-stu-id="da147-719">Yes</span></span>|<span data-ttu-id="da147-720">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-720">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-721">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="da147-721">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="da147-722">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-722">statusDescription</span></span>|<span data-ttu-id="da147-723">字串</span><span class="sxs-lookup"><span data-stu-id="da147-723">string</span></span>|<span data-ttu-id="da147-724">否</span><span class="sxs-lookup"><span data-stu-id="da147-724">No</span></span>|<span data-ttu-id="da147-725">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-725">Description of hello status.</span></span>|  
  
### <a name="remove-rule"></a><span data-ttu-id="da147-726">移除規則</span><span class="sxs-lookup"><span data-stu-id="da147-726">Remove Rule</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-727">要求</span><span class="sxs-lookup"><span data-stu-id="da147-727">Request</span></span>  

<span data-ttu-id="da147-728">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-728">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-729">Key</span><span class="sxs-lookup"><span data-stu-id="da147-729">Key</span></span>|<span data-ttu-id="da147-730">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-730">Value Type</span></span>|<span data-ttu-id="da147-731">必要</span><span class="sxs-lookup"><span data-stu-id="da147-731">Required</span></span>|<span data-ttu-id="da147-732">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-732">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-733">operation</span><span class="sxs-lookup"><span data-stu-id="da147-733">operation</span></span>|<span data-ttu-id="da147-734">字串</span><span class="sxs-lookup"><span data-stu-id="da147-734">string</span></span>|<span data-ttu-id="da147-735">是</span><span class="sxs-lookup"><span data-stu-id="da147-735">Yes</span></span>|`com.microsoft:remove-rule`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-736">uint</span><span class="sxs-lookup"><span data-stu-id="da147-736">uint</span></span>|<span data-ttu-id="da147-737">否</span><span class="sxs-lookup"><span data-stu-id="da147-737">No</span></span>|<span data-ttu-id="da147-738">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-738">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-739">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-739">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-740">Key</span><span class="sxs-lookup"><span data-stu-id="da147-740">Key</span></span>|<span data-ttu-id="da147-741">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-741">Value Type</span></span>|<span data-ttu-id="da147-742">必要</span><span class="sxs-lookup"><span data-stu-id="da147-742">Required</span></span>|<span data-ttu-id="da147-743">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-743">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-744">rule-name</span><span class="sxs-lookup"><span data-stu-id="da147-744">rule-name</span></span>|<span data-ttu-id="da147-745">字串</span><span class="sxs-lookup"><span data-stu-id="da147-745">string</span></span>|<span data-ttu-id="da147-746">是</span><span class="sxs-lookup"><span data-stu-id="da147-746">Yes</span></span>|<span data-ttu-id="da147-747">規則名稱，不包括訂用帳戶和主題名稱。</span><span class="sxs-lookup"><span data-stu-id="da147-747">Rule name, not including subscription and topic names.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-748">Response</span><span class="sxs-lookup"><span data-stu-id="da147-748">Response</span></span>  

<span data-ttu-id="da147-749">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-749">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-750">Key</span><span class="sxs-lookup"><span data-stu-id="da147-750">Key</span></span>|<span data-ttu-id="da147-751">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-751">Value Type</span></span>|<span data-ttu-id="da147-752">必要</span><span class="sxs-lookup"><span data-stu-id="da147-752">Required</span></span>|<span data-ttu-id="da147-753">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-753">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-754">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-754">statusCode</span></span>|<span data-ttu-id="da147-755">int</span><span class="sxs-lookup"><span data-stu-id="da147-755">int</span></span>|<span data-ttu-id="da147-756">是</span><span class="sxs-lookup"><span data-stu-id="da147-756">Yes</span></span>|<span data-ttu-id="da147-757">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-757">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-758">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="da147-758">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="da147-759">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-759">statusDescription</span></span>|<span data-ttu-id="da147-760">字串</span><span class="sxs-lookup"><span data-stu-id="da147-760">string</span></span>|<span data-ttu-id="da147-761">否</span><span class="sxs-lookup"><span data-stu-id="da147-761">No</span></span>|<span data-ttu-id="da147-762">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-762">Description of hello status.</span></span>|  
  
## <a name="deferred-message-operations"></a><span data-ttu-id="da147-763">延遲的訊息作業</span><span class="sxs-lookup"><span data-stu-id="da147-763">Deferred message operations</span></span>  
  
### <a name="receive-by-sequence-number"></a><span data-ttu-id="da147-764">依照序號接收</span><span class="sxs-lookup"><span data-stu-id="da147-764">Receive by sequence number</span></span>  

<span data-ttu-id="da147-765">依序號接收延遲的訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-765">Receives deferred messages by sequence number.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-766">要求</span><span class="sxs-lookup"><span data-stu-id="da147-766">Request</span></span>  

<span data-ttu-id="da147-767">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-767">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-768">Key</span><span class="sxs-lookup"><span data-stu-id="da147-768">Key</span></span>|<span data-ttu-id="da147-769">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-769">Value Type</span></span>|<span data-ttu-id="da147-770">必要</span><span class="sxs-lookup"><span data-stu-id="da147-770">Required</span></span>|<span data-ttu-id="da147-771">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-771">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-772">operation</span><span class="sxs-lookup"><span data-stu-id="da147-772">operation</span></span>|<span data-ttu-id="da147-773">字串</span><span class="sxs-lookup"><span data-stu-id="da147-773">string</span></span>|<span data-ttu-id="da147-774">是</span><span class="sxs-lookup"><span data-stu-id="da147-774">Yes</span></span>|`com.microsoft:receive-by-sequence-number`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-775">uint</span><span class="sxs-lookup"><span data-stu-id="da147-775">uint</span></span>|<span data-ttu-id="da147-776">否</span><span class="sxs-lookup"><span data-stu-id="da147-776">No</span></span>|<span data-ttu-id="da147-777">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-777">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-778">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-778">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-779">Key</span><span class="sxs-lookup"><span data-stu-id="da147-779">Key</span></span>|<span data-ttu-id="da147-780">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-780">Value Type</span></span>|<span data-ttu-id="da147-781">必要</span><span class="sxs-lookup"><span data-stu-id="da147-781">Required</span></span>|<span data-ttu-id="da147-782">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-782">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-783">sequence-numbers</span><span class="sxs-lookup"><span data-stu-id="da147-783">sequence-numbers</span></span>|<span data-ttu-id="da147-784">長整數的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-784">array of long</span></span>|<span data-ttu-id="da147-785">是</span><span class="sxs-lookup"><span data-stu-id="da147-785">Yes</span></span>|<span data-ttu-id="da147-786">序號。</span><span class="sxs-lookup"><span data-stu-id="da147-786">Sequence numbers.</span></span>|  
|<span data-ttu-id="da147-787">receiver-settle-mode</span><span class="sxs-lookup"><span data-stu-id="da147-787">receiver-settle-mode</span></span>|<span data-ttu-id="da147-788">ubyte</span><span class="sxs-lookup"><span data-stu-id="da147-788">ubyte</span></span>|<span data-ttu-id="da147-789">是</span><span class="sxs-lookup"><span data-stu-id="da147-789">Yes</span></span>|<span data-ttu-id="da147-790">AMQP 核心 1.0 版中所指定的「收件者支付」模式。</span><span class="sxs-lookup"><span data-stu-id="da147-790">**Receiver settle** mode as specified in AMQP core v1.0.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-791">Response</span><span class="sxs-lookup"><span data-stu-id="da147-791">Response</span></span>  

<span data-ttu-id="da147-792">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-792">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-793">Key</span><span class="sxs-lookup"><span data-stu-id="da147-793">Key</span></span>|<span data-ttu-id="da147-794">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-794">Value Type</span></span>|<span data-ttu-id="da147-795">必要</span><span class="sxs-lookup"><span data-stu-id="da147-795">Required</span></span>|<span data-ttu-id="da147-796">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-796">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-797">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-797">statusCode</span></span>|<span data-ttu-id="da147-798">int</span><span class="sxs-lookup"><span data-stu-id="da147-798">int</span></span>|<span data-ttu-id="da147-799">是</span><span class="sxs-lookup"><span data-stu-id="da147-799">Yes</span></span>|<span data-ttu-id="da147-800">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-800">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-801">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="da147-801">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="da147-802">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-802">statusDescription</span></span>|<span data-ttu-id="da147-803">字串</span><span class="sxs-lookup"><span data-stu-id="da147-803">string</span></span>|<span data-ttu-id="da147-804">否</span><span class="sxs-lookup"><span data-stu-id="da147-804">No</span></span>|<span data-ttu-id="da147-805">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-805">Description of hello status.</span></span>|  
  
<span data-ttu-id="da147-806">hello 回應訊息內文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-806">hello response message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-807">Key</span><span class="sxs-lookup"><span data-stu-id="da147-807">Key</span></span>|<span data-ttu-id="da147-808">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-808">Value Type</span></span>|<span data-ttu-id="da147-809">必要</span><span class="sxs-lookup"><span data-stu-id="da147-809">Required</span></span>|<span data-ttu-id="da147-810">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-810">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-811">上限</span><span class="sxs-lookup"><span data-stu-id="da147-811">messages</span></span>|<span data-ttu-id="da147-812">對應的清單</span><span class="sxs-lookup"><span data-stu-id="da147-812">list of maps</span></span>|<span data-ttu-id="da147-813">是</span><span class="sxs-lookup"><span data-stu-id="da147-813">Yes</span></span>|<span data-ttu-id="da147-814">當中每個對應都代表一則訊息的訊息清單。</span><span class="sxs-lookup"><span data-stu-id="da147-814">List of messages where every map represents a message.</span></span>|  
  
<span data-ttu-id="da147-815">hello 對應表示訊息必須包含下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-815">hello map representing a message must contain hello following entries:</span></span>  
  
|<span data-ttu-id="da147-816">Key</span><span class="sxs-lookup"><span data-stu-id="da147-816">Key</span></span>|<span data-ttu-id="da147-817">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-817">Value Type</span></span>|<span data-ttu-id="da147-818">必要</span><span class="sxs-lookup"><span data-stu-id="da147-818">Required</span></span>|<span data-ttu-id="da147-819">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-819">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-820">lock-token</span><span class="sxs-lookup"><span data-stu-id="da147-820">lock-token</span></span>|<span data-ttu-id="da147-821">uuid</span><span class="sxs-lookup"><span data-stu-id="da147-821">uuid</span></span>|<span data-ttu-id="da147-822">是</span><span class="sxs-lookup"><span data-stu-id="da147-822">Yes</span></span>|<span data-ttu-id="da147-823">如果 `receiver-settle-mode` 為 1 則鎖定權杖。</span><span class="sxs-lookup"><span data-stu-id="da147-823">Lock token if `receiver-settle-mode` is 1.</span></span>|  
|<span data-ttu-id="da147-824">訊息</span><span class="sxs-lookup"><span data-stu-id="da147-824">message</span></span>|<span data-ttu-id="da147-825">位元組的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-825">array of byte</span></span>|<span data-ttu-id="da147-826">是</span><span class="sxs-lookup"><span data-stu-id="da147-826">Yes</span></span>|<span data-ttu-id="da147-827">AMQP 1.0 連線編碼訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-827">AMQP 1.0 wire-encoded message.</span></span>|  
  
### <a name="update-disposition-status"></a><span data-ttu-id="da147-828">更新配置狀態</span><span class="sxs-lookup"><span data-stu-id="da147-828">Update disposition status</span></span>  

<span data-ttu-id="da147-829">更新 hello 配置狀態延後的訊息。</span><span class="sxs-lookup"><span data-stu-id="da147-829">Updates hello disposition status of deferred messages.</span></span>  
  
#### <a name="request"></a><span data-ttu-id="da147-830">要求</span><span class="sxs-lookup"><span data-stu-id="da147-830">Request</span></span>  

<span data-ttu-id="da147-831">hello 要求訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-831">hello request message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-832">Key</span><span class="sxs-lookup"><span data-stu-id="da147-832">Key</span></span>|<span data-ttu-id="da147-833">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-833">Value Type</span></span>|<span data-ttu-id="da147-834">必要</span><span class="sxs-lookup"><span data-stu-id="da147-834">Required</span></span>|<span data-ttu-id="da147-835">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-835">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-836">operation</span><span class="sxs-lookup"><span data-stu-id="da147-836">operation</span></span>|<span data-ttu-id="da147-837">字串</span><span class="sxs-lookup"><span data-stu-id="da147-837">string</span></span>|<span data-ttu-id="da147-838">是</span><span class="sxs-lookup"><span data-stu-id="da147-838">Yes</span></span>|`com.microsoft:update-disposition`|  
|`com.microsoft:server-timeout`|<span data-ttu-id="da147-839">uint</span><span class="sxs-lookup"><span data-stu-id="da147-839">uint</span></span>|<span data-ttu-id="da147-840">否</span><span class="sxs-lookup"><span data-stu-id="da147-840">No</span></span>|<span data-ttu-id="da147-841">作業伺服器逾時以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="da147-841">Operation server timeout in milliseconds.</span></span>|  
  
<span data-ttu-id="da147-842">hello 要求訊息本文必須包含**amqp 值**> 一節包含**對應**以 hello 下列項目：</span><span class="sxs-lookup"><span data-stu-id="da147-842">hello request message body must consist of an **amqp-value** section containing a **map** with hello following entries:</span></span>  
  
|<span data-ttu-id="da147-843">Key</span><span class="sxs-lookup"><span data-stu-id="da147-843">Key</span></span>|<span data-ttu-id="da147-844">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-844">Value Type</span></span>|<span data-ttu-id="da147-845">必要</span><span class="sxs-lookup"><span data-stu-id="da147-845">Required</span></span>|<span data-ttu-id="da147-846">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-846">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-847">disposition-status</span><span class="sxs-lookup"><span data-stu-id="da147-847">disposition-status</span></span>|<span data-ttu-id="da147-848">string</span><span class="sxs-lookup"><span data-stu-id="da147-848">string</span></span>|<span data-ttu-id="da147-849">是</span><span class="sxs-lookup"><span data-stu-id="da147-849">Yes</span></span>|<span data-ttu-id="da147-850">完成</span><span class="sxs-lookup"><span data-stu-id="da147-850">completed</span></span><br /><br /> <span data-ttu-id="da147-851">放棄</span><span class="sxs-lookup"><span data-stu-id="da147-851">abandoned</span></span><br /><br /> <span data-ttu-id="da147-852">暫止</span><span class="sxs-lookup"><span data-stu-id="da147-852">suspended</span></span>|  
|<span data-ttu-id="da147-853">lock-tokens</span><span class="sxs-lookup"><span data-stu-id="da147-853">lock-tokens</span></span>|<span data-ttu-id="da147-854">UUID 的陣列</span><span class="sxs-lookup"><span data-stu-id="da147-854">array of uuid</span></span>|<span data-ttu-id="da147-855">是</span><span class="sxs-lookup"><span data-stu-id="da147-855">Yes</span></span>|<span data-ttu-id="da147-856">訊息鎖定權杖 tooupdate 配置狀態。</span><span class="sxs-lookup"><span data-stu-id="da147-856">Message lock tokens tooupdate disposition status.</span></span>|  
|<span data-ttu-id="da147-857">deadletter-reason</span><span class="sxs-lookup"><span data-stu-id="da147-857">deadletter-reason</span></span>|<span data-ttu-id="da147-858">字串</span><span class="sxs-lookup"><span data-stu-id="da147-858">string</span></span>|<span data-ttu-id="da147-859">否</span><span class="sxs-lookup"><span data-stu-id="da147-859">No</span></span>|<span data-ttu-id="da147-860">如果設定太配置狀態可能會設定**暫停**。</span><span class="sxs-lookup"><span data-stu-id="da147-860">May be set if disposition status is set too**suspended**.</span></span>|  
|<span data-ttu-id="da147-861">deadletter-description</span><span class="sxs-lookup"><span data-stu-id="da147-861">deadletter-description</span></span>|<span data-ttu-id="da147-862">字串</span><span class="sxs-lookup"><span data-stu-id="da147-862">string</span></span>|<span data-ttu-id="da147-863">否</span><span class="sxs-lookup"><span data-stu-id="da147-863">No</span></span>|<span data-ttu-id="da147-864">如果設定太配置狀態可能會設定**暫停**。</span><span class="sxs-lookup"><span data-stu-id="da147-864">May be set if disposition status is set too**suspended**.</span></span>|  
|<span data-ttu-id="da147-865">properties-to-modify</span><span class="sxs-lookup"><span data-stu-id="da147-865">properties-to-modify</span></span>|<span data-ttu-id="da147-866">map</span><span class="sxs-lookup"><span data-stu-id="da147-866">map</span></span>|<span data-ttu-id="da147-867">否</span><span class="sxs-lookup"><span data-stu-id="da147-867">No</span></span>|<span data-ttu-id="da147-868">清單中的服務匯流排代理訊息屬性 toomodify。</span><span class="sxs-lookup"><span data-stu-id="da147-868">List of Service Bus brokered message properties toomodify.</span></span>|  
  
#### <a name="response"></a><span data-ttu-id="da147-869">Response</span><span class="sxs-lookup"><span data-stu-id="da147-869">Response</span></span>  

<span data-ttu-id="da147-870">hello 回應訊息必須包含下列應用程式屬性的 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-870">hello response message must include hello following application properties:</span></span>  
  
|<span data-ttu-id="da147-871">Key</span><span class="sxs-lookup"><span data-stu-id="da147-871">Key</span></span>|<span data-ttu-id="da147-872">值類型</span><span class="sxs-lookup"><span data-stu-id="da147-872">Value Type</span></span>|<span data-ttu-id="da147-873">必要</span><span class="sxs-lookup"><span data-stu-id="da147-873">Required</span></span>|<span data-ttu-id="da147-874">值內容</span><span class="sxs-lookup"><span data-stu-id="da147-874">Value Contents</span></span>|  
|---------|----------------|--------------|--------------------|  
|<span data-ttu-id="da147-875">StatusCode</span><span class="sxs-lookup"><span data-stu-id="da147-875">statusCode</span></span>|<span data-ttu-id="da147-876">int</span><span class="sxs-lookup"><span data-stu-id="da147-876">int</span></span>|<span data-ttu-id="da147-877">是</span><span class="sxs-lookup"><span data-stu-id="da147-877">Yes</span></span>|<span data-ttu-id="da147-878">HTTP 回應碼 [RFC2616]</span><span class="sxs-lookup"><span data-stu-id="da147-878">HTTP response code [RFC2616]</span></span><br /><br /> <span data-ttu-id="da147-879">200：確定 – 成功，否則失敗</span><span class="sxs-lookup"><span data-stu-id="da147-879">200: OK – success, otherwise failed</span></span>|  
|<span data-ttu-id="da147-880">statusDescription</span><span class="sxs-lookup"><span data-stu-id="da147-880">statusDescription</span></span>|<span data-ttu-id="da147-881">字串</span><span class="sxs-lookup"><span data-stu-id="da147-881">string</span></span>|<span data-ttu-id="da147-882">否</span><span class="sxs-lookup"><span data-stu-id="da147-882">No</span></span>|<span data-ttu-id="da147-883">Hello 狀態的描述。</span><span class="sxs-lookup"><span data-stu-id="da147-883">Description of hello status.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="da147-884">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da147-884">Next steps</span></span>

<span data-ttu-id="da147-885">深入了解 AMQP 和 Service Bus toolearn 請造訪下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="da147-885">toolearn more about AMQP and Service Bus, visit hello following links:</span></span>

* <span data-ttu-id="da147-886">[服務匯流排 AMQP 概觀]</span><span class="sxs-lookup"><span data-stu-id="da147-886">[Service Bus AMQP overview]</span></span>
* <span data-ttu-id="da147-887">[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]</span><span class="sxs-lookup"><span data-stu-id="da147-887">[AMQP 1.0 support for Service Bus partitioned queues and topics]</span></span>
* <span data-ttu-id="da147-888">[Windows Server 服務匯流排中的 AMQP]</span><span class="sxs-lookup"><span data-stu-id="da147-888">[AMQP in Service Bus for Windows Server]</span></span>

[服務匯流排 AMQP 概觀]: service-bus-amqp-overview.md
[適用於服務匯流排分割的佇列和主題的 AMQP 1.0 支援]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[Windows Server 服務匯流排中的 AMQP]: https://msdn.microsoft.com/library/dn574799.asp