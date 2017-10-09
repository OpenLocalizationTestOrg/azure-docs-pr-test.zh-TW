---
title: "aaaService 匯流排定價和計費 |Microsoft 文件"
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
ms.openlocfilehash: 4d06fe015baba45fef04e198363447c5541d1724
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-pricing-and-billing"></a><span data-ttu-id="f4891-103">服務匯流排定價與計費</span><span class="sxs-lookup"><span data-stu-id="f4891-103">Service Bus pricing and billing</span></span>
<span data-ttu-id="f4891-104">服務匯流排提供基本、標準和[進階](service-bus-premium-messaging.md)層。</span><span class="sxs-lookup"><span data-stu-id="f4891-104">Service Bus is offered in Basic, Standard, and [Premium](service-bus-premium-messaging.md) tiers.</span></span> <span data-ttu-id="f4891-105">您可以針對建立的每個服務匯流排服務命名空間選擇一個服務層，此選取層會套用至該命名空間內建立的所有實體。</span><span class="sxs-lookup"><span data-stu-id="f4891-105">You can choose a service tier for each Service Bus service namespace that you create, and this tier selection applies across all entities created within that namespace.</span></span>

> [!NOTE]
> <span data-ttu-id="f4891-106">如需目前服務匯流排定價的詳細資訊，請參閱 hello [Azure 服務匯流排定價頁面](https://azure.microsoft.com/pricing/details/service-bus/)，和 hello [Service Bus 常見問題集](service-bus-faq.md#pricing)。</span><span class="sxs-lookup"><span data-stu-id="f4891-106">For detailed information about current Service Bus pricing, see hello [Azure Service Bus pricing page](https://azure.microsoft.com/pricing/details/service-bus/), and hello [Service Bus FAQ](service-bus-faq.md#pricing).</span></span>
>
>

<span data-ttu-id="f4891-107">服務匯流排會使用下列兩個計量器佇列和主題/訂閱 hello:</span><span class="sxs-lookup"><span data-stu-id="f4891-107">Service Bus uses hello following two meters for queues and topics/subscriptions:</span></span>

1. <span data-ttu-id="f4891-108">**傳訊作業**：定義為針對佇列或主題/訂用帳戶服務端點的 API 呼叫。</span><span class="sxs-lookup"><span data-stu-id="f4891-108">**Messaging Operations**: Defined as API calls against queue or topic/subscription service endpoints.</span></span> <span data-ttu-id="f4891-109">此計量器將取代傳送或收到 hello 主要單元的可計費的使用量，對佇列和主題/訂閱訊息。</span><span class="sxs-lookup"><span data-stu-id="f4891-109">This meter will replace messages sent or received as hello primary unit of billable usage for queues and topics/subscriptions.</span></span>
2. <span data-ttu-id="f4891-110">**代理連線**： 定義為 hello 尖峰數目持續連線開啟針對佇列、 主題或訂用帳戶在指定的一小時取樣期間內。</span><span class="sxs-lookup"><span data-stu-id="f4891-110">**Brokered Connections**: Defined as hello peak number of persistent connections open against queues, topics, or subscriptions during a given one-hour sampling period.</span></span> <span data-ttu-id="f4891-111">這個計費表只會套用在 hello 標準層次中，您可以在其中開啟其他連接 （連接之前，每個佇列/主題/訂閱的有限的 too100） 名義上的每個連線費用。</span><span class="sxs-lookup"><span data-stu-id="f4891-111">This meter will only apply in hello Standard tier, in which you can open additional connections (previously, connections were limited too100 per queue/topic/subscription) for a nominal per-connection fee.</span></span>

<span data-ttu-id="f4891-112">hello**標準**層批量與佇列和主題/訂閱，導致磁碟區為基礎的折扣的 too80 %hello 最高使用量層級執行的作業。</span><span class="sxs-lookup"><span data-stu-id="f4891-112">hello **Standard** tier introduces graduated pricing for operations performed with queues and topics/subscriptions, resulting in volume-based discounts of up too80% at hello highest usage levels.</span></span> <span data-ttu-id="f4891-113">此外，還有每個月，可讓您 tooperform too12.5 百萬個作業，每個月免費 $ 10 美元的標準層基本費。</span><span class="sxs-lookup"><span data-stu-id="f4891-113">There is also a Standard tier base charge of $10 per month, which enables you tooperform up too12.5 million operations per month at no additional cost.</span></span>

<span data-ttu-id="f4891-114">hello **Premium**層提供資源隔離層 hello CPU 和記憶體，以便在隔離狀態執行的每個客戶工作負載。</span><span class="sxs-lookup"><span data-stu-id="f4891-114">hello **Premium** tier provides resource isolation at hello CPU and memory layer so that each customer workload runs in isolation.</span></span> <span data-ttu-id="f4891-115">此資源容器稱為「傳訊單位」 。</span><span class="sxs-lookup"><span data-stu-id="f4891-115">This resource container is called a *messaging unit*.</span></span> <span data-ttu-id="f4891-116">每個進階命名空間都會被配置至少一個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="f4891-116">Each premium namespace is allocated at least one messaging unit.</span></span> <span data-ttu-id="f4891-117">您可以為每個服務匯流排進階命名空間購買 1、2 或 4 個傳訊單位。</span><span class="sxs-lookup"><span data-stu-id="f4891-117">You can purchase 1, 2, or 4 messaging units for each Service Bus Premium namespace.</span></span> <span data-ttu-id="f4891-118">單一的工作負載或實體可以跨越多個傳訊單位，可在將變更 hello 傳訊單位數目，雖然計費是 24 小時或每日速率費用。</span><span class="sxs-lookup"><span data-stu-id="f4891-118">A single workload or entity can span multiple messaging units and hello number of messaging units can be changed at will, although billing is in 24-hour or daily rate charges.</span></span> <span data-ttu-id="f4891-119">hello 結果是您 Service Bus 為基礎的解決方案的效能可預測且可重複。</span><span class="sxs-lookup"><span data-stu-id="f4891-119">hello result is predictable and repeatable performance for your Service Bus-based solution.</span></span> <span data-ttu-id="f4891-120">此效能不僅更可預測並可取得，而且還更快速。</span><span class="sxs-lookup"><span data-stu-id="f4891-120">Not only is this performance more predictable and available, but it is also faster.</span></span>

<span data-ttu-id="f4891-121">請注意，每個 Azure 訂用帳戶每月一次計費 hello 標準層基本費。</span><span class="sxs-lookup"><span data-stu-id="f4891-121">Note that hello Standard tier base charge is charged only once per month per Azure subscription.</span></span> <span data-ttu-id="f4891-122">這表示您建立單一標準層的服務匯流排命名空間之後，您將會無法 toocreate 許多其他標準命名空間為您想在該相同的 Azure 訂用帳戶，而不會產生其他基底的費用。</span><span class="sxs-lookup"><span data-stu-id="f4891-122">This means that after you create a single Standard tier Service Bus namespace, you will be able toocreate as many additional Standard namespaces as you want under that same Azure subscription, without incurring additional base charges.</span></span>

<span data-ttu-id="f4891-123">hello[服務匯流排定價](https://azure.microsoft.com/pricing/details/service-bus/)表摘要說明 hello hello Basic、 Standard 和 Premium 層之間的功能差異。</span><span class="sxs-lookup"><span data-stu-id="f4891-123">hello [Service Bus pricing](https://azure.microsoft.com/pricing/details/service-bus/) table summarizes hello functional differences between hello Basic, Standard, and Premium tiers.</span></span>

## <a name="messaging-operations"></a><span data-ttu-id="f4891-124">傳訊作業</span><span class="sxs-lookup"><span data-stu-id="f4891-124">Messaging operations</span></span>
<span data-ttu-id="f4891-125">Hello 新計價模型的一部分，變更的佇列和主題/訂閱計費。</span><span class="sxs-lookup"><span data-stu-id="f4891-125">As part of hello new pricing model, billing for queues and topics/subscriptions is changing.</span></span> <span data-ttu-id="f4891-126">這些實體會從每個每個作業的訊息 toobilling 計費轉換。</span><span class="sxs-lookup"><span data-stu-id="f4891-126">These entities are transitioning from billing per message toobilling per operation.</span></span> <span data-ttu-id="f4891-127">「 作業 」 是指 tooany API 進行呼叫時，對佇列或主題/訂閱服務端點。</span><span class="sxs-lookup"><span data-stu-id="f4891-127">An "operation" refers tooany API call made against a queue or topic/subscription service endpoint.</span></span> <span data-ttu-id="f4891-128">這包括管理、傳送/接收和工作階段狀態的作業。</span><span class="sxs-lookup"><span data-stu-id="f4891-128">This includes management, send/receive, and session state operations.</span></span>

| <span data-ttu-id="f4891-129">作業類型</span><span class="sxs-lookup"><span data-stu-id="f4891-129">Operation Type</span></span> | <span data-ttu-id="f4891-130">說明</span><span class="sxs-lookup"><span data-stu-id="f4891-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4891-131">管理</span><span class="sxs-lookup"><span data-stu-id="f4891-131">Management</span></span> |<span data-ttu-id="f4891-132">對佇列或主題/訂用帳戶執行的建立、讀取、更新、刪除 (CRUD)。</span><span class="sxs-lookup"><span data-stu-id="f4891-132">Create, Read, Update, Delete (CRUD) against queues or topics/subscriptions.</span></span> |
| <span data-ttu-id="f4891-133">訊息</span><span class="sxs-lookup"><span data-stu-id="f4891-133">Messaging</span></span> |<span data-ttu-id="f4891-134">用佇列或主題/訂用帳戶傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="f4891-134">Sending and receiving messages with queues or topics/subscriptions.</span></span> |
| <span data-ttu-id="f4891-135">工作階段狀態</span><span class="sxs-lookup"><span data-stu-id="f4891-135">Session state</span></span> |<span data-ttu-id="f4891-136">取得或設定佇列或主題/訂用帳戶上的工作階段狀態。</span><span class="sxs-lookup"><span data-stu-id="f4891-136">Getting or setting session state on a queue or topic/subscription.</span></span> |

<span data-ttu-id="f4891-137">成本的詳細資訊，請參閱列在 hello hello 價格[服務匯流排定價](https://azure.microsoft.com/pricing/details/service-bus/)頁面。</span><span class="sxs-lookup"><span data-stu-id="f4891-137">For cost details, see hello prices listed on hello [Service Bus pricing](https://azure.microsoft.com/pricing/details/service-bus/) page.</span></span>

## <a name="brokered-connections"></a><span data-ttu-id="f4891-138">代理連線</span><span class="sxs-lookup"><span data-stu-id="f4891-138">Brokered connections</span></span>
<span data-ttu-id="f4891-139">*Brokered connections* 內含的客戶使用量模式，牽涉到針對佇列、主題或訂用帳戶而「持續連線」的大量傳送者/接收者。</span><span class="sxs-lookup"><span data-stu-id="f4891-139">*Brokered connections* accommodate customer usage patterns that involve a large number of "persistently connected" senders/receivers against queues, topics, or subscriptions.</span></span> <span data-ttu-id="f4891-140">持續連線的傳送者/接收者是指使用 AMQP 或 HTTP 進行連線，且接收逾時為非零值 (例如 HTTP 長時間輪詢) 的對象。</span><span class="sxs-lookup"><span data-stu-id="f4891-140">Persistently connected senders/receivers are those that connect using either AMQP or HTTP with a non-zero receive timeout (for example, HTTP long polling).</span></span> <span data-ttu-id="f4891-141">具有立即逾時的 HTTP 傳送者和接收者並不會產生代理連線。</span><span class="sxs-lookup"><span data-stu-id="f4891-141">HTTP senders and receivers with an immediate timeout do not generate brokered connections.</span></span>

<span data-ttu-id="f4891-142">連線配額及其他服務限制，請參閱 hello [Service Bus 配額](service-bus-quotas.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="f4891-142">For connection quotas and other service limits, see hello [Service Bus quotas](service-bus-quotas.md) article.</span></span>

<span data-ttu-id="f4891-143">hello 標準層移除 hello 命名空間每個代理的連線限制，並計算代理的連線使用量跨 hello Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f4891-143">hello Standard tier removes hello per-namespace brokered connection limit and counts aggregate brokered connection usage across hello Azure subscription.</span></span> <span data-ttu-id="f4891-144">如需詳細資訊，請參閱 hello[代理連線](https://azure.microsoft.com/pricing/details/service-bus/)資料表。</span><span class="sxs-lookup"><span data-stu-id="f4891-144">For more information, see hello [Brokered connections](https://azure.microsoft.com/pricing/details/service-bus/) table.</span></span>

> [!NOTE]
> <span data-ttu-id="f4891-145">1,000 個代理的連線隨附與 hello 標準訊息層級 （透過 hello 基本費），而且可以橫跨所有佇列、 主題和訂用帳戶相關聯的 hello Azure 訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="f4891-145">1,000 brokered connections are included with hello Standard messaging tier (via hello base charge) and can be shared across all queues, topics, and subscriptions within hello associated Azure subscription.</span></span>
>
>

<br />

> [!NOTE]
> <span data-ttu-id="f4891-146">計費根據並行連線的 hello 尖峰數目和每小時根據每月 744 小時按比例。</span><span class="sxs-lookup"><span data-stu-id="f4891-146">Billing is based on hello peak number of concurrent connections and is prorated hourly based on 744 hours per month.</span></span>
>
>

| <span data-ttu-id="f4891-147">高階層</span><span class="sxs-lookup"><span data-stu-id="f4891-147">Premium Tier</span></span> |
| --- |
| <span data-ttu-id="f4891-148">代理的連線不會向 hello Premium 層中。</span><span class="sxs-lookup"><span data-stu-id="f4891-148">Brokered connections are not charged in hello Premium tier.</span></span> |

<span data-ttu-id="f4891-149">如需代理連線的詳細資訊，請參閱 hello[常見問題集](#faq)本主題稍後的章節。</span><span class="sxs-lookup"><span data-stu-id="f4891-149">For more information about brokered connections, see hello [FAQ](#faq) section later in this topic.</span></span>

## <a name="faq"></a><span data-ttu-id="f4891-150">常見問題集</span><span class="sxs-lookup"><span data-stu-id="f4891-150">FAQ</span></span>

### <a name="what-are-brokered-connections-and-how-do-i-get-charged-for-them"></a><span data-ttu-id="f4891-151">什麼是代理連線，以及如何支付它們的費用？</span><span class="sxs-lookup"><span data-stu-id="f4891-151">What are brokered connections and how do I get charged for them?</span></span>
<span data-ttu-id="f4891-152">代理的連線的定義 hello 下列其中一種：</span><span class="sxs-lookup"><span data-stu-id="f4891-152">A brokered connection is defined as one of hello following:</span></span>

1. <span data-ttu-id="f4891-153">來自用戶端 tooa Service Bus 佇列或主題/訂閱的 AMQP 連線。</span><span class="sxs-lookup"><span data-stu-id="f4891-153">An AMQP connection from a client tooa Service Bus queue or topic/subscription.</span></span>
2. <span data-ttu-id="f4891-154">HTTP 呼叫 tooreceive 訊息從服務匯流排主題或佇列接收逾時值大於零。</span><span class="sxs-lookup"><span data-stu-id="f4891-154">An HTTP call tooreceive a message from a Service Bus topic or queue that has a receive timeout value greater than zero.</span></span>

<span data-ttu-id="f4891-155">服務匯流排 hello 尖峰數目超過 hello 的並行代理連線費用包含數量 （hello 標準層中為 1,000 個）。</span><span class="sxs-lookup"><span data-stu-id="f4891-155">Service Bus charges for hello peak number of concurrent brokered connections that exceed hello included quantity (1,000 in hello Standard tier).</span></span> <span data-ttu-id="f4891-156">每小時測量，除以中一個月 744 小時來按比例和加總每月計費週期的 hello 透過尖峰。</span><span class="sxs-lookup"><span data-stu-id="f4891-156">Peaks are measured on an hourly basis, prorated by dividing by 744 hours in a month, and added up over hello monthly billing period.</span></span> <span data-ttu-id="f4891-157">在針對 hello hello 依比例每小時尖峰總數 hello 計費期的 hello 結束套用 hello 包含數量 （每個月的 1,000 個代理連線）。</span><span class="sxs-lookup"><span data-stu-id="f4891-157">hello included quantity (1,000 brokered connections per month) is applied at hello end of hello billing period against hello sum of hello prorated hourly peaks.</span></span>

<span data-ttu-id="f4891-158">例如：</span><span class="sxs-lookup"><span data-stu-id="f4891-158">For example:</span></span>

1. <span data-ttu-id="f4891-159">10,000 台裝置均透過單一 AMQP 連線進行連線，並接收來自服務匯流排主題的命令。</span><span class="sxs-lookup"><span data-stu-id="f4891-159">Each of 10,000 devices connects via a single AMQP connection, and receives commands from a Service Bus topic.</span></span> <span data-ttu-id="f4891-160">hello 裝置傳送遙測事件 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="f4891-160">hello devices send telemetry events tooan Event Hub.</span></span> <span data-ttu-id="f4891-161">如果所有裝置都連線 12 小時內每一天，將套用下列連線費用的 hello (加法 tooany 中其他的服務匯流排主題費用): 10,000 個連線 * 12 小時 * 31 天 / 744 = 5,000 個代理連線。</span><span class="sxs-lookup"><span data-stu-id="f4891-161">If all devices connect for 12 hours each day, hello following connection charges apply (in addition tooany other Service Bus topic charges): 10,000 connections * 12 hours * 31 days / 744 = 5,000 brokered connections.</span></span> <span data-ttu-id="f4891-162">Hello 每月額度 1,000 個代理連線之後, 您收取 4,000 個代理連線，速率為每個代理連線，總計 $120 個 $0.03 hello。</span><span class="sxs-lookup"><span data-stu-id="f4891-162">After hello monthly allowance of 1,000 brokered connections, you would be charged for 4,000 brokered connections, at hello rate of $0.03 per brokered connection, for a total of $120.</span></span>
2. <span data-ttu-id="f4891-163">10,000 台裝置透過 HTTP 從服務匯流排佇列接收訊息，並指定非零的逾時值。</span><span class="sxs-lookup"><span data-stu-id="f4891-163">10,000 devices receive messages from a Service Bus queue via HTTP, specifying a non-zero timeout.</span></span> <span data-ttu-id="f4891-164">如果所有裝置都連線 12 小時內每一天，您會看到下列連線費用 hello (加法 tooany 中其他的服務匯流排費用): 10,000 個 HTTP 接收連線 * 每天 12 小時 * 31 天/744 小時 = 5,000 個代理連線。</span><span class="sxs-lookup"><span data-stu-id="f4891-164">If all devices connect for 12 hours every day, you will see hello following connection charges (in addition tooany other Service Bus charges): 10,000 HTTP Receive connections * 12 hours per day * 31 days / 744 hours = 5,000 brokered connections.</span></span>

### <a name="do-brokered-connection-charges-apply-tooqueues-and-topicssubscriptions"></a><span data-ttu-id="f4891-165">代理的連線費用套用 tooqueues 和主題/訂閱嗎？</span><span class="sxs-lookup"><span data-stu-id="f4891-165">Do brokered connection charges apply tooqueues and topics/subscriptions?</span></span>
<span data-ttu-id="f4891-166">是。</span><span class="sxs-lookup"><span data-stu-id="f4891-166">Yes.</span></span> <span data-ttu-id="f4891-167">沒有任何使用 HTTP，不論 hello 多少傳送系統與裝置的事件傳送的連線費用。</span><span class="sxs-lookup"><span data-stu-id="f4891-167">There are no connection charges for sending events using HTTP, regardless of hello number of sending systems or devices.</span></span> <span data-ttu-id="f4891-168">使用逾時大於零的 HTTP 來接收事件，有時也稱為「長時間輪詢」，會產生代理連線的費用。</span><span class="sxs-lookup"><span data-stu-id="f4891-168">Receiving events with HTTP using a timeout greater than zero, sometimes called "long polling," generates brokered connection charges.</span></span> <span data-ttu-id="f4891-169">AMQP 連線都會產生代理的連線費用，無論 hello 連線正在使用的 toosend 或接收。</span><span class="sxs-lookup"><span data-stu-id="f4891-169">AMQP connections generate brokered connection charges regardless of whether hello connections are being used toosend or receive.</span></span> <span data-ttu-id="f4891-170">請注意，在基本層命名空間中，可以免費使用 100 個代理連線。</span><span class="sxs-lookup"><span data-stu-id="f4891-170">Note that 100 brokered connections are allowed at no charge in a Basic namespace.</span></span> <span data-ttu-id="f4891-171">這也是 hello hello Azure 訂用帳戶所允許的代理連線的數目上限。</span><span class="sxs-lookup"><span data-stu-id="f4891-171">This is also hello maximum number of brokered connections allowed for hello Azure subscription.</span></span> <span data-ttu-id="f4891-172">hello 個 Azure 訂用帳戶中的所有標準命名空間的前 1,000 個代理的連線是包含在任何額外的收費 （除了基本費 hello）。</span><span class="sxs-lookup"><span data-stu-id="f4891-172">hello first 1,000 brokered connections across all Standard namespaces in an Azure subscription are included at no extra charge (beyond hello base charge).</span></span> <span data-ttu-id="f4891-173">因為這些額度足以 toocover 許多服務對服務傳訊案例中，代理的連線費用通常就要注意如果您計劃大量用戶端; toouse AMQP 或 HTTP 長期輪詢例如，tooachieve 效率事件資料流或啟用雙向通訊對許多裝置或應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="f4891-173">Because these allowances are enough toocover many service-to-service messaging scenarios, brokered connection charges usually only become relevant if you plan toouse AMQP or HTTP long-polling with a large number of clients; for example, tooachieve more efficient event streaming or enable bi-directional communication with many devices or application instances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4891-174">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f4891-174">Next steps</span></span>
* <span data-ttu-id="f4891-175">如需服務匯流排定價的完整詳細資訊，請參閱 hello[服務匯流排定價頁面](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="f4891-175">For complete details about Service Bus pricing, see hello [Service Bus pricing page](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>
* <span data-ttu-id="f4891-176">請參閱 hello [Service Bus 常見問題集](service-bus-faq.md#pricing)的一些常見的常見問題集有關服務匯流排定價和計費。</span><span class="sxs-lookup"><span data-stu-id="f4891-176">See hello [Service Bus FAQ](service-bus-faq.md#pricing) for some common FAQs about Service bus pricing and billing.</span></span>

[Azure portal]: https://portal.azure.com
