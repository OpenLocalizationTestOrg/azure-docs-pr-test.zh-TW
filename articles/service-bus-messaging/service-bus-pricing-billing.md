---
title: "服務匯流排定價與計費 | Microsoft Docs"
description: "服務匯流排定價結構的概觀。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7c45b112-e911-45ab-9203-a2e5abccd6e0
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/02/2017
ms.author: sethm
ms.openlocfilehash: 5161b555db96886f556a4fe96eab4415d8ccf047
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-bus-pricing-and-billing"></a><span data-ttu-id="0d1eb-103">服務匯流排定價與計費</span><span class="sxs-lookup"><span data-stu-id="0d1eb-103">Service Bus pricing and billing</span></span>
<span data-ttu-id="0d1eb-104">服務匯流排提供基本、標準和[進階](service-bus-premium-messaging.md)層。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-104">Service Bus is offered in Basic, Standard, and [Premium](service-bus-premium-messaging.md) tiers.</span></span> <span data-ttu-id="0d1eb-105">您可以針對建立的每個服務匯流排服務命名空間選擇一個服務層，此選取層會套用至該命名空間內建立的所有實體。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-105">You can choose a service tier for each Service Bus service namespace that you create, and this tier selection applies across all entities created within that namespace.</span></span>

> [!NOTE]
> <span data-ttu-id="0d1eb-106">如需目前服務匯流排的價格詳細資訊，請參閱 [Azure 服務匯流排價格頁面](https://azure.microsoft.com/pricing/details/service-bus/)和[服務匯流排常見問題集](service-bus-faq.md#pricing)。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-106">For detailed information about current Service Bus pricing, see the [Azure Service Bus pricing page](https://azure.microsoft.com/pricing/details/service-bus/), and the [Service Bus FAQ](service-bus-faq.md#pricing).</span></span>
>
>

<span data-ttu-id="0d1eb-107">服務匯流排會在佇列和主題/訂用帳戶中使用下列兩種計量：</span><span class="sxs-lookup"><span data-stu-id="0d1eb-107">Service Bus uses the following two meters for queues and topics/subscriptions:</span></span>

1. <span data-ttu-id="0d1eb-108">**傳訊作業**：定義為針對佇列或主題/訂用帳戶服務端點的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-108">**Messaging Operations**: Defined as API calls against queue or topic/subscription service endpoints.</span></span> <span data-ttu-id="0d1eb-109">這個計量將取代送出或收到的訊息數，成為佇列和主題/訂用帳戶中可計費使用量的主要單位。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-109">This meter will replace messages sent or received as the primary unit of billable usage for queues and topics/subscriptions.</span></span>
2. <span data-ttu-id="0d1eb-110">**代理連線**：定義為在指定的一小時取樣期間，針對佇列、主題或訂用帳戶開啟的持續連線尖峰數量。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-110">**Brokered Connections**: Defined as the peak number of persistent connections open against queues, topics, or subscriptions during a given one-hour sampling period.</span></span> <span data-ttu-id="0d1eb-111">這個計量只會套用至標準層，您可以在其中開啟其他連線 (之前的連線限制為每個佇列/主題/訂用帳戶 100 個)，支付每個連線的額定費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-111">This meter will only apply in the Standard tier, in which you can open additional connections (previously, connections were limited to 100 per queue/topic/subscription) for a nominal per-connection fee.</span></span>

<span data-ttu-id="0d1eb-112">**標準** 層為搭配佇列和主題/訂用帳戶執行的作業引進了漸進式定價，使得以量計價型折扣在最高使用量層級上可高達 80%。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-112">The **Standard** tier introduces graduated pricing for operations performed with queues and topics/subscriptions, resulting in volume-based discounts of up to 80% at the highest usage levels.</span></span> <span data-ttu-id="0d1eb-113">另外還有每個月 $10 美元的標準層基本費用，讓您每個月執行最多 1,250 萬個作業，且不需額外費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-113">There is also a Standard tier base charge of $10 per month, which enables you to perform up to 12.5 million operations per month at no additional cost.</span></span>

<span data-ttu-id="0d1eb-114">**高階** 層可讓您在 CPU 和記憶體層隔離資源，讓每個客戶工作負載能獨立執行。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-114">The **Premium** tier provides resource isolation at the CPU and memory layer so that each customer workload runs in isolation.</span></span> <span data-ttu-id="0d1eb-115">此資源容器稱為「傳訊單位」 。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-115">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="0d1eb-116">每個進階命名空間都會被配置至少一個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-116">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="0d1eb-117">您可以為每個服務匯流排進階命名空間購買 1、2 或 4 個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-117">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="0d1eb-118">單一工作負載或實體可以跨越多個傳訊單位，而傳訊單位數目可以隨意變更，雖然計費是依 24 小時或每日費率收費。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-118">A single workload or entity can span multiple messaging units and the number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="0d1eb-119">結果是您的服務匯流排方案的效能可預測並可重複。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-119">The result is predictable and repeatable performance for your Service Bus-based solution.</span></span> <span data-ttu-id="0d1eb-120">此效能不僅更可預測並可取得，而且還更快速。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-120">Not only is this performance more predictable and available, but it is also faster.</span></span>

<span data-ttu-id="0d1eb-121">請注意，對於每個 Azure 訂用帳戶，每個月只收取一次標準層基本費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-121">Note that the Standard tier base charge is charged only once per month per Azure subscription.</span></span> <span data-ttu-id="0d1eb-122">這表示建立單一標準層服務匯流排命名空間之後，您就可以在同一個 Azure 訂用帳戶下，依需要建立更多標準層命名空間，而不必支付額外的基本費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-122">This means that after you create a single Standard tier Service Bus namespace, you will be able to create as many additional Standard namespaces as you want under that same Azure subscription, without incurring additional base charges.</span></span>

<span data-ttu-id="0d1eb-123">[服務匯流排價格](https://azure.microsoft.com/pricing/details/service-bus/)表格摘要說明基本層、標準層和進階層之間的功能差異。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-123">The [Service Bus pricing](https://azure.microsoft.com/pricing/details/service-bus/) table summarizes the functional differences between the Basic, Standard, and Premium tiers.</span></span>

## <a name="messaging-operations"></a><span data-ttu-id="0d1eb-124">傳訊作業</span><span class="sxs-lookup"><span data-stu-id="0d1eb-124">Messaging operations</span></span>
<span data-ttu-id="0d1eb-125">在新定價模型中，佇列和主題/訂用帳戶的計費方式正在改變。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-125">As part of the new pricing model, billing for queues and topics/subscriptions is changing.</span></span> <span data-ttu-id="0d1eb-126">這些實體會從每則訊息計費轉換成每個作業計費。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-126">These entities are transitioning from billing per message to billing per operation.</span></span> <span data-ttu-id="0d1eb-127">「作業」指的是針對佇列或主題/訂用帳戶服務端點所建立的任何 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-127">An "operation" refers to any API call made against a queue or topic/subscription service endpoint.</span></span> <span data-ttu-id="0d1eb-128">這包括管理、傳送/接收和工作階段狀態的作業。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-128">This includes management, send/receive, and session state operations.</span></span>

| <span data-ttu-id="0d1eb-129">作業類型</span><span class="sxs-lookup"><span data-stu-id="0d1eb-129">Operation Type</span></span> | <span data-ttu-id="0d1eb-130">說明</span><span class="sxs-lookup"><span data-stu-id="0d1eb-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0d1eb-131">管理</span><span class="sxs-lookup"><span data-stu-id="0d1eb-131">Management</span></span> |<span data-ttu-id="0d1eb-132">對佇列或主題/訂用帳戶執行的建立、讀取、更新、刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-132">Create, Read, Update, Delete (CRUD) against queues or topics/subscriptions.</span></span> |
| <span data-ttu-id="0d1eb-133">訊息</span><span class="sxs-lookup"><span data-stu-id="0d1eb-133">Messaging</span></span> |<span data-ttu-id="0d1eb-134">用佇列或主題/訂用帳戶傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-134">Sending and receiving messages with queues or topics/subscriptions.</span></span> |
| <span data-ttu-id="0d1eb-135">工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="0d1eb-135">Session state</span></span> |<span data-ttu-id="0d1eb-136">取得或設定佇列或主題/訂用帳戶上的工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-136">Getting or setting session state on a queue or topic/subscription.</span></span> |

<span data-ttu-id="0d1eb-137">如需成本的詳細資訊，請參閱[服務匯流排價格](https://azure.microsoft.com/pricing/details/service-bus/)頁面列出的價格。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-137">For cost details, see the prices listed on the [Service Bus pricing](https://azure.microsoft.com/pricing/details/service-bus/) page.</span></span>

## <a name="brokered-connections"></a><span data-ttu-id="0d1eb-138">代理連線</span><span class="sxs-lookup"><span data-stu-id="0d1eb-138">Brokered connections</span></span>
<span data-ttu-id="0d1eb-139">*Brokered connections* 內含的客戶使用量模式，牽涉到針對佇列、主題或訂用帳戶而「持續連線」的大量傳送者/接收者。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-139">*Brokered connections* accommodate customer usage patterns that involve a large number of "persistently connected" senders/receivers against queues, topics, or subscriptions.</span></span> <span data-ttu-id="0d1eb-140">持續連線的傳送者/接收者是指使用 AMQP 或 HTTP 進行連線，且接收逾時為非零值 (例如 HTTP 長時間輪詢) 的對象。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-140">Persistently connected senders/receivers are those that connect using either AMQP or HTTP with a non-zero receive timeout (for example, HTTP long polling).</span></span> <span data-ttu-id="0d1eb-141">具有立即逾時的 HTTP 傳送者和接收者並不會產生代理連線。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-141">HTTP senders and receivers with an immediate timeout do not generate brokered connections.</span></span>

<span data-ttu-id="0d1eb-142">關於連線配額和其他服務限制，請參閱[服務匯流排配額](service-bus-quotas.md)一文。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-142">For connection quotas and other service limits, see the [Service Bus quotas](service-bus-quotas.md) article.</span></span>

<span data-ttu-id="0d1eb-143">標準層會移除每個命名空間的代理連線限制，並計算 Azure 訂用帳戶上彙總的代理連線使用量。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-143">The Standard tier removes the per-namespace brokered connection limit and counts aggregate brokered connection usage across the Azure subscription.</span></span> <span data-ttu-id="0d1eb-144">如需詳細資訊，請參閱[代理連線](https://azure.microsoft.com/pricing/details/service-bus/)表格。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-144">For more information, see the [Brokered connections](https://azure.microsoft.com/pricing/details/service-bus/) table.</span></span>

> [!NOTE]
> <span data-ttu-id="0d1eb-145">標準傳訊層隨附 1,000 個代理連線 (包含在基本費用內)，而且可以在相關聯的 Azure 訂用帳戶內，讓所有佇列、主題和訂用帳戶共用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-145">1,000 brokered connections are included with the Standard messaging tier (via the base charge) and can be shared across all queues, topics, and subscriptions within the associated Azure subscription.</span></span>
>
>

<br />

> [!NOTE]
> <span data-ttu-id="0d1eb-146">計費會依據並行連線的尖峰數量，並以每個月 744 小時為基礎，按照每小時的比例計算。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-146">Billing is based on the peak number of concurrent connections and is prorated hourly based on 744 hours per month.</span></span>
>
>

| <span data-ttu-id="0d1eb-147">高階層</span><span class="sxs-lookup"><span data-stu-id="0d1eb-147">Premium Tier</span></span> |
| --- |
| <span data-ttu-id="0d1eb-148">在高階層中，不對代理連線收費。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-148">Brokered connections are not charged in the Premium tier.</span></span> |

<span data-ttu-id="0d1eb-149">如需關於代理連線的詳細資訊，請參閱本主題稍後的 [常見問題集](#faq) 一節。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-149">For more information about brokered connections, see the [FAQ](#faq) section later in this topic.</span></span>

## <a name="faq"></a><span data-ttu-id="0d1eb-150">常見問題集</span><span class="sxs-lookup"><span data-stu-id="0d1eb-150">FAQ</span></span>

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a><span data-ttu-id="0d1eb-151">什麼是代理連線，以及如何支付它們的費用？</span><span class="sxs-lookup"><span data-stu-id="0d1eb-151">What are brokered connections and how do I get charged for them?</span></span>
<span data-ttu-id="0d1eb-152">代理連線可定義為下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="0d1eb-152">A brokered connection is defined as one of the following:</span></span>

1. <span data-ttu-id="0d1eb-153">從用戶端到服務匯流排佇列或主題/訂用帳戶的 AMQP 連線。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-153">An AMQP connection from a client to a Service Bus queue or topic/subscription.</span></span>
2. <span data-ttu-id="0d1eb-154">從服務匯流排主題或佇列接收訊息的 HTTP 呼叫，且接收的逾時值大於零。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-154">An HTTP call to receive a message from a Service Bus topic or queue that has a receive timeout value greater than zero.</span></span>

<span data-ttu-id="0d1eb-155">服務匯流排的並行代理連線尖峰數量，如果超過隨附數量 (標準層中為 1,000 個)，就會收取費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-155">Service Bus charges for the peak number of concurrent brokered connections that exceed the included quantity (1,000 in the Standard tier).</span></span> <span data-ttu-id="0d1eb-156">尖峰的測量方式會以每小時為基礎，除以每個月的 744 小時來依比例計算，並依據每個月的計費期間來加總。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-156">Peaks are measured on an hourly basis, prorated by dividing by 744 hours in a month, and added up over the monthly billing period.</span></span> <span data-ttu-id="0d1eb-157">隨附的數量 (每個月 1,000 個代理連線) 會根據依比例計算的每小時尖峰的總和，在計費期間快結束時加以套用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-157">The included quantity (1,000 brokered connections per month) is applied at the end of the billing period against the sum of the prorated hourly peaks.</span></span>

<span data-ttu-id="0d1eb-158">例如：</span><span class="sxs-lookup"><span data-stu-id="0d1eb-158">For example:</span></span>

1. <span data-ttu-id="0d1eb-159">10,000 台裝置均透過單一 AMQP 連線進行連線，並接收來自服務匯流排主題的命令。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-159">Each of 10,000 devices connects via a single AMQP connection, and receives commands from a Service Bus topic.</span></span> <span data-ttu-id="0d1eb-160">裝置將遙測事件傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-160">The devices send telemetry events to an Event Hub.</span></span> <span data-ttu-id="0d1eb-161">如果所有裝置每天都連線 12 小時，則除了其他服務匯流排的任何主題費用外，還會有以下連線費用：10,000 個連線 * 12 小時 * 31 天 / 744 = 5,000 個代理連線。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-161">If all devices connect for 12 hours each day, the following connection charges apply (in addition to any other Service Bus topic charges): 10,000 connections * 12 hours * 31 days / 744 = 5,000 brokered connections.</span></span> <span data-ttu-id="0d1eb-162">超過每月 1,000 個代理連線的額度後，就會以每個代理連線 $0.03 美元的費率，對 4,000 個代理連線收費，總共 $120 美元。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-162">After the monthly allowance of 1,000 brokered connections, you would be charged for 4,000 brokered connections, at the rate of $0.03 per brokered connection, for a total of $120.</span></span>
2. <span data-ttu-id="0d1eb-163">10,000 台裝置透過 HTTP 從服務匯流排佇列接收訊息，並指定非零的逾時值。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-163">10,000 devices receive messages from a Service Bus queue via HTTP, specifying a non-zero timeout.</span></span> <span data-ttu-id="0d1eb-164">如果所有裝置每天都連線 12 小時，則除了其他服務匯流排的任何費用外，您還會看到以下連線費用：10,000 個 HTTP 接收連線 * 每天 12 小時 * 31 天 / 744 = 5,000 個代理連線。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-164">If all devices connect for 12 hours every day, you will see the following connection charges (in addition to any other Service Bus charges): 10,000 HTTP Receive connections * 12 hours per day * 31 days / 744 hours = 5,000 brokered connections.</span></span>

### <a name="do-brokered-connection-charges-apply-to-queues-and-topicssubscriptions"></a><span data-ttu-id="0d1eb-165">佇列和主題/訂用帳戶需要代理連線費用嗎？</span><span class="sxs-lookup"><span data-stu-id="0d1eb-165">Do brokered connection charges apply to queues and topics/subscriptions?</span></span>
<span data-ttu-id="0d1eb-166">是。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-166">Yes.</span></span> <span data-ttu-id="0d1eb-167">不論傳送系統或裝置的數目多寡，使用 HTTP 來傳送事件不需要支付連線費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-167">There are no connection charges for sending events using HTTP, regardless of the number of sending systems or devices.</span></span> <span data-ttu-id="0d1eb-168">使用逾時大於零的 HTTP 來接收事件，有時也稱為「長時間輪詢」，會產生代理連線的費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-168">Receiving events with HTTP using a timeout greater than zero, sometimes called "long polling," generates brokered connection charges.</span></span> <span data-ttu-id="0d1eb-169">AMQP 連線均會產生代理連線費用，不論連線是用於傳送或接收皆然。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-169">AMQP connections generate brokered connection charges regardless of whether the connections are being used to send or receive.</span></span> <span data-ttu-id="0d1eb-170">請注意，在基本層命名空間中，可以免費使用 100 個代理連線。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-170">Note that 100 brokered connections are allowed at no charge in a Basic namespace.</span></span> <span data-ttu-id="0d1eb-171">這也是 Azure 訂用帳戶允許的代理連線數目上限。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-171">This is also the maximum number of brokered connections allowed for the Azure subscription.</span></span> <span data-ttu-id="0d1eb-172">在 Azure 訂用帳戶中，所有標準層命名空間內的前 1,000 個代理連線，除了基本費用外，均不需額外費用。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-172">The first 1,000 brokered connections across all Standard namespaces in an Azure subscription are included at no extra charge (beyond the base charge).</span></span> <span data-ttu-id="0d1eb-173">因為這些額度便足以涵蓋許多服務對服務的傳訊案例，通常只在您打算使用 AMQP 或 HTTP 的長時間輪詢加上大量用戶端時，才可能會有相應的代理連線費用。例如，想要達到更有效率的事件資料流，或啟用與許多裝置或應用程式執行個體間的雙向通訊。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-173">Because these allowances are enough to cover many service-to-service messaging scenarios, brokered connection charges usually only become relevant if you plan to use AMQP or HTTP long-polling with a large number of clients; for example, to achieve more efficient event streaming or enable bi-directional communication with many devices or application instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d1eb-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d1eb-174">Next steps</span></span>
* <span data-ttu-id="0d1eb-175">如需服務匯流排價格的完整詳細資訊，請參閱[服務匯流排價格頁面](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-175">For complete details about Service Bus pricing, see the [Service Bus pricing page](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>
* <span data-ttu-id="0d1eb-176">關於服務匯流排價格與計費的一些常見問題集，請參閱[服務匯流排常見問題集](service-bus-faq.md#pricing)。</span><span class="sxs-lookup"><span data-stu-id="0d1eb-176">See the [Service Bus FAQ](service-bus-faq.md#pricing) for some common FAQs about Service bus pricing and billing.</span></span>

[Azure portal]: https://portal.azure.com
