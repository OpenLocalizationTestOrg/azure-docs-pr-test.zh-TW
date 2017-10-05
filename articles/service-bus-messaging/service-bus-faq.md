---
title: "Azure 服務匯流排常見問題集 (FAQ) | Microsoft Docs"
description: "回答一些有關 Azure 服務匯流排的常見問題。"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 1403184d96388cb03b2c767c4da342ec1c6fe236
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-faq"></a><span data-ttu-id="9d4fd-103">服務匯流排常見問題集</span><span class="sxs-lookup"><span data-stu-id="9d4fd-103">Service Bus FAQ</span></span>
<span data-ttu-id="9d4fd-104">本文提供 Microsoft Azure 服務匯流排的一些常見問題解集。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-104">This article answers some frequently asked questions about Microsoft Azure Service Bus.</span></span> <span data-ttu-id="9d4fd-105">您也可以造訪 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)，以取得一般的 Azure 價格和支援資訊。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-105">You can also visit the [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span>

## <a name="general-questions-about-azure-service-bus"></a><span data-ttu-id="9d4fd-106">關於 Azure 服務匯流排的一般問題</span><span class="sxs-lookup"><span data-stu-id="9d4fd-106">General questions about Azure Service Bus</span></span>
### <a name="what-is-azure-service-bus"></a><span data-ttu-id="9d4fd-107">什麼是 Azure 服務匯流排？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-107">What is Azure Service Bus?</span></span>
<span data-ttu-id="9d4fd-108">[Azure 服務匯流排](service-bus-messaging-overview.md)是非同步的訊息雲端平台，可讓您在彼此分離的系統之間傳送資料。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-108">[Azure Service Bus](service-bus-messaging-overview.md) is an asynchronous messaging cloud platform that enables you to send data between decoupled systems.</span></span> <span data-ttu-id="9d4fd-109">Microsoft 以服務的形式提供此功能，這表示您不需要裝載任何自有硬體就能使用。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-109">Microsoft offers this feature as a service, which means that you do not need to host any of your own hardware in order to use it.</span></span>

### <a name="what-is-a-service-bus-namespace"></a><span data-ttu-id="9d4fd-110">什麼是服務匯流排命名空間？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-110">What is a Service Bus namespace?</span></span>
<span data-ttu-id="9d4fd-111">[命名空間](service-bus-create-namespace-portal.md)提供範圍容器，可在應用程式內定址服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-111">A [namespace](service-bus-create-namespace-portal.md) provides a scoping container for addressing Service Bus resources within your application.</span></span> <span data-ttu-id="9d4fd-112">必須建立命名空間才能使用服務匯流排，而且這也是開始使用的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-112">Creating one is necessary to use Service Bus and will be one of the first steps in getting started.</span></span>

### <a name="what-is-an-azure-service-bus-queue"></a><span data-ttu-id="9d4fd-113">什麼是 Azure 服務匯流排佇列？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-113">What is an Azure Service Bus queue?</span></span>
<span data-ttu-id="9d4fd-114">[服務匯流排佇列](service-bus-queues-topics-subscriptions.md)是訊息儲存所在的實體。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-114">A [Service Bus queue](service-bus-queues-topics-subscriptions.md) is an entity in which messages are stored.</span></span> <span data-ttu-id="9d4fd-115">如果您有多個應用程式，或多個需要彼此通訊的分散式應用程式部分，佇列會特別有用。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-115">Queues are particularly useful when you have multiple applications, or multiple parts of a distributed application that need to communicate with each other.</span></span> <span data-ttu-id="9d4fd-116">佇列和配送中心的類似之處在於，兩者都會接收多個產品 (訊息)，再從該處送出。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-116">The queue is similar to a distribution center in that multiple products (messages) are received and then sent from that location.</span></span>

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a><span data-ttu-id="9d4fd-117">什麼是 Azure 服務匯流排主題和訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-117">What are Azure Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="9d4fd-118">主題可視覺化為佇列，而且在使用多個訂用帳戶時，主題會變成更豐富的訊息模型；基本上是一對多的通訊工具。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-118">A topic can be visualized as a queue and when using multiple subscriptions, it becomes a richer messaging model; essentially a one-to-many communication tool.</span></span> <span data-ttu-id="9d4fd-119">此發佈/訂閱模型 (或「pub/sub」) 可讓應用程式將訊息傳送至具有多個訂用帳戶的主題，以便讓多個應用程式接收該訊息。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-119">This publish/subscribe model (or *pub/sub*) enables an application that sends a message to a topic with multiple subscriptions to have that message received by multiple applications.</span></span>

### <a name="what-is-a-partitioned-entity"></a><span data-ttu-id="9d4fd-120">什麼是分割的實體？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-120">What is a partitioned entity?</span></span>
<span data-ttu-id="9d4fd-121">傳統的佇列或主題由單一訊息代理程式處理並儲存在一個訊息存放區中。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-121">A conventional queue or topic is handled by a single message broker and stored in one messaging store.</span></span> <span data-ttu-id="9d4fd-122">[分割的佇列或主題](service-bus-partitioning.md)會由多個訊息代理程式處理，並儲存在多個訊息存放區。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-122">A [partitioned queue or topic](service-bus-partitioning.md) is handled by multiple message brokers and stored in multiple messaging stores.</span></span> <span data-ttu-id="9d4fd-123">這表示分割佇列或主題的整體輸送量不會再受到單一訊息代理程式或訊息存放區的效能所限制。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-123">This means that the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="9d4fd-124">此外，即使訊息存放區暫時中斷也不會讓分割的佇列或主題無法使用。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-124">In addition, a temporary outage of a messaging store does not render a partitioned queue or topic unavailable.</span></span>

<span data-ttu-id="9d4fd-125">請注意，使用分割實體時無法確保順序。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-125">Note that ordering is not ensured when using partitioning entities.</span></span> <span data-ttu-id="9d4fd-126">若分割無法使用，您仍可從其他分割傳送及接收訊息。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-126">In the event that a partition is unavailable, you can still send and receive messages from the other partitions.</span></span>

## <a name="best-practices"></a><span data-ttu-id="9d4fd-127">最佳作法</span><span class="sxs-lookup"><span data-stu-id="9d4fd-127">Best practices</span></span>
### <a name="what-are-some-azure-service-bus-best-practices"></a><span data-ttu-id="9d4fd-128">Azure 服務匯流排的最佳做法有哪些？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-128">What are some Azure Service Bus best practices?</span></span>
* <span data-ttu-id="9d4fd-129">[使用服務匯流排的效能改進最佳作法][Best practices for performance improvements using Service Bus] - 這篇文章說明如何在交換訊息時將效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-129">[Best practices for performance improvements using Service Bus][Best practices for performance improvements using Service Bus] – this article describes how to optimize performance when exchanging messages.</span></span>

### <a name="what-should-i-know-before-creating-entities"></a><span data-ttu-id="9d4fd-130">建立實體前的須知事項為何？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-130">What should I know before creating entities?</span></span>
<span data-ttu-id="9d4fd-131">佇列和主題的下列屬性是不可變的。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-131">The following properties of a queue and topic are immutable.</span></span> <span data-ttu-id="9d4fd-132">在佈建實體時請將這一點納入考量，因為若要修改屬性，就必須建立新的替代實體。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-132">Please take this into account when you provision your entities as this cannot be modified, without creating a new replacement entity.</span></span>

* <span data-ttu-id="9d4fd-133">大小</span><span class="sxs-lookup"><span data-stu-id="9d4fd-133">Size</span></span>
* <span data-ttu-id="9d4fd-134">分割</span><span class="sxs-lookup"><span data-stu-id="9d4fd-134">Partitioning</span></span>
* <span data-ttu-id="9d4fd-135">工作階段</span><span class="sxs-lookup"><span data-stu-id="9d4fd-135">Sessions</span></span>
* <span data-ttu-id="9d4fd-136">重複偵測</span><span class="sxs-lookup"><span data-stu-id="9d4fd-136">Duplicate detection</span></span>
* <span data-ttu-id="9d4fd-137">快速實體</span><span class="sxs-lookup"><span data-stu-id="9d4fd-137">Express entity</span></span>

## <a name="pricing"></a><span data-ttu-id="9d4fd-138">價格</span><span class="sxs-lookup"><span data-stu-id="9d4fd-138">Pricing</span></span>
<span data-ttu-id="9d4fd-139">本節提供服務匯流排價格結構的一些常見問題解答。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-139">This section answers some frequently-asked questions about the Service Bus pricing structure.</span></span>

<span data-ttu-id="9d4fd-140">[服務匯流排價格和計費](service-bus-pricing-billing.md)一文說明服務匯流排中的計費計量，如需服務匯流排價格選項的相關資訊，請參閱[服務匯流排價格詳細資料](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-140">The [Service Bus pricing and billing](service-bus-pricing-billing.md) article explains the billing meters in Service Bus, and for information about Service Bus pricing options, see [Service Bus pricing details](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>

<span data-ttu-id="9d4fd-141">您也可以造訪 [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)，以取得一般 Azure 價格資訊。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-141">You can also visit the [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing information.</span></span> 

### <a name="how-do-you-charge-for-service-bus"></a><span data-ttu-id="9d4fd-142">服務匯流排的收費方式為何？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-142">How do you charge for Service Bus?</span></span>
<span data-ttu-id="9d4fd-143">如需服務匯流排價格的完整資訊，請參閱[服務匯流排價格詳細資料][Pricing overview]。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-143">For complete information about Service Bus pricing, please see [Service Bus pricing details][Pricing overview].</span></span> <span data-ttu-id="9d4fd-144">除了註明的價格，您還需支付您的應用程式佈建所在資料中心外部的輸出相關資料傳輸費用。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-144">In addition to the prices noted, you are charged for associated data transfers for egress outside of the data center in which your application is provisioned.</span></span>

### <a name="what-usage-of-service-bus-is-subject-to-data-transfer-what-is-not"></a><span data-ttu-id="9d4fd-145">何種服務匯流排用法需支付資料傳輸費用？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-145">What usage of Service Bus is subject to data transfer?</span></span> <span data-ttu-id="9d4fd-146">何種不需？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-146">What is not?</span></span>
<span data-ttu-id="9d4fd-147">指定的 Azure 區域內的任何資料傳輸都是免費提供，以及任何輸入的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-147">Any data transfer within a given Azure region is provided at no charge, as well as any inbound data transfer.</span></span> <span data-ttu-id="9d4fd-148">區域外部的資料傳送需要出口流量費用，可以在[這裡](https://azure.microsoft.com/pricing/details/bandwidth/)找到。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-148">Data transfer outside a region is subject to egress charges which can be found [here](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="does-service-bus-charge-for-storage"></a><span data-ttu-id="9d4fd-149">服務匯流排是否會收取儲存體費用？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-149">Does Service Bus charge for storage?</span></span>
<span data-ttu-id="9d4fd-150">不會，服務匯流排不會收取儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-150">No, Service Bus does not charge for storage.</span></span> <span data-ttu-id="9d4fd-151">不過，有配額會限制每個佇列/主題可保存的資料數量上限。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-151">However, there is a quota limiting the maximum amount of data that can be persisted per queue/topic.</span></span> <span data-ttu-id="9d4fd-152">請參閱下一個常見問題。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-152">See the next FAQ.</span></span>

## <a name="quotas"></a><span data-ttu-id="9d4fd-153">配額</span><span class="sxs-lookup"><span data-stu-id="9d4fd-153">Quotas</span></span>

<span data-ttu-id="9d4fd-154">如需服務匯流排限制和配額的清單，請參閱[服務匯流排配額概觀][Quotas overview]。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-154">For a list of Service Bus limits and quotas, see the [Service Bus quotas overview][Quotas overview].</span></span>

### <a name="does-service-bus-have-any-usage-quotas"></a><span data-ttu-id="9d4fd-155">服務匯流排是否有任何使用量配額？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-155">Does Service Bus have any usage quotas?</span></span>
<span data-ttu-id="9d4fd-156">根據預設，對於所有雲端服務，Microsoft 會設定針對所有客戶的訂用帳戶計算的彙總每月使用量配額。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-156">By default, for any cloud service Microsoft sets an aggregate monthly usage quota that is calculated across all of a customer's subscriptions.</span></span> <span data-ttu-id="9d4fd-157">因為我們了解您的需求可能超過這些限制，請隨時連絡客戶服務部門，讓我們能夠了解您的需求並適當地調整這些限制。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-157">Because we understand that you may need more than these limits, please contact customer service at any time so that we can understand your needs and adjust these limits appropriately.</span></span> <span data-ttu-id="9d4fd-158">針對服務匯流排，彙總使用量配額為每個月 50 億則訊息。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-158">For Service Bus, the aggregate usage quota is 5 billion messages per month.</span></span>

<span data-ttu-id="9d4fd-159">雖然我們有權停用在指定的月份內超出其使用量配額的客戶帳戶，但我們將提供電子郵件通知並且在採取任何動作之前多次嘗試連絡客戶。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-159">While we do reserve the right to disable a customer account that has exceeded its usage quotas in a given month, we will provide e-mail notification and make multiple attempts to contact a customer before taking any action.</span></span> <span data-ttu-id="9d4fd-160">超出這些配額的客戶仍需負責支付超出配額的費用。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-160">Customers exceeding these quotas will still be responsible for charges that exceed the quotas.</span></span>

<span data-ttu-id="9d4fd-161">如同 Azure 上的其他服務，服務匯流排會強制執行一組特定的配額，以確保公平的資源使用量。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-161">As with other services on Azure, Service Bus enforces a set of specific quotas to ensure that there is fair usage of resources.</span></span> <span data-ttu-id="9d4fd-162">您可以在[服務匯流排配額概觀][Quotas overview]中找到更多關於這些配額的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-162">You can find more details about these quotas in the [Service Bus quotas overview][Quotas overview].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9d4fd-163">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9d4fd-163">Troubleshooting</span></span>
### <a name="what-are-some-of-the-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a><span data-ttu-id="9d4fd-164">Azure 服務匯流排 API 所產生的例外狀況有哪些，其建議的動作為何？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-164">What are some of the exceptions generated by Azure Service Bus APIs and their suggested actions?</span></span>
<span data-ttu-id="9d4fd-165">如需可能的服務匯流排例外狀況，請參閱[例外狀況概觀][Exceptions overview]。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-165">For a list of possible Service Bus exceptions, see [Exceptions overview][Exceptions overview].</span></span>

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a><span data-ttu-id="9d4fd-166">什麼是共用存取簽章，何種語言可支援產生簽章？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-166">What is a Shared Access Signature and which languages support generating a signature?</span></span>
<span data-ttu-id="9d4fd-167">共用存取簽章是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-167">Shared Access Signatures are an authentication mechanism based on SHA – 256 secure hashes or URIs.</span></span> <span data-ttu-id="9d4fd-168">如需如何以 Node、PHP、Java 和 C\# 產生自有簽章的相關資訊，請參閱[共用存取簽章][Shared Access Signatures]一文。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-168">For information about how to generate your own signatures in Node, PHP, Java and C\#, see the [Shared Access Signatures][Shared Access Signatures] article.</span></span>

## <a name="subscription-and-namespace-management"></a><span data-ttu-id="9d4fd-169">訂用帳戶和命名空間管理</span><span class="sxs-lookup"><span data-stu-id="9d4fd-169">Subscription and namespace management</span></span>
### <a name="how-do-i-migrate-a-namespace-to-another-azure-subscription"></a><span data-ttu-id="9d4fd-170">如何將命名空間移轉到另一個 Azure 訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="9d4fd-170">How do I migrate a namespace to another Azure subscription?</span></span>

<span data-ttu-id="9d4fd-171">您可以使用 [Azure 入口網站](https://portal.azure.com)或 PowerShell 命令，將命名空間從一個 Azure 訂用帳戶移到另一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-171">You can move a namespace from one Azure subscription to another, using either the [Azure portal](https://portal.azure.com) or PowerShell commands.</span></span> <span data-ttu-id="9d4fd-172">若要執行此作業，命名空間必須已是作用中。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-172">In order to execute the operation, the namespace must already be active.</span></span> <span data-ttu-id="9d4fd-173">執行命令的使用者必須同時是來源和目標訂用帳戶上的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-173">The user executing the commands must be an administrator on both the source and target subscriptions.</span></span>

#### <a name="portal"></a><span data-ttu-id="9d4fd-174">入口網站</span><span class="sxs-lookup"><span data-stu-id="9d4fd-174">Portal</span></span>

<span data-ttu-id="9d4fd-175">若要使用 Azure 入口網站將「服務匯流排」移到另一個訂用帳戶，請依照[這裡](../azure-resource-manager/resource-group-move-resources.md#use-portal)的指示操作。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-175">To use the Azure portal to migrate Service Bus namespaces to another subscription, follow the directions [here](../azure-resource-manager/resource-group-move-resources.md#use-portal).</span></span> 

#### <a name="powershell"></a><span data-ttu-id="9d4fd-176">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d4fd-176">PowerShell</span></span>

<span data-ttu-id="9d4fd-177">下列 PowerShell 命令序列會將命名空間從一個 Azure 訂用帳戶移到另一個訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-177">The following sequence of PowerShell commands moves a namespace from one Azure subscription to another.</span></span> <span data-ttu-id="9d4fd-178">若要執行這項作業，命名空間必須已經是作用中，而且執行 PowerShell 命令的使用者必須是來源與目標訂用帳戶的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-178">To execute this operation, the namespace must already be active, and the user running the PowerShell commands must be an administrator on both the source and target subscriptions.</span></span>

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription to target subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a><span data-ttu-id="9d4fd-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d4fd-179">Next steps</span></span>
<span data-ttu-id="9d4fd-180">若要深入了解服務匯流排，請參閱下列主題。</span><span class="sxs-lookup"><span data-stu-id="9d4fd-180">To learn more about Service Bus, see the following topics.</span></span>

* [<span data-ttu-id="9d4fd-181">Azure 服務匯流排進階簡介 (部落格文章)</span><span class="sxs-lookup"><span data-stu-id="9d4fd-181">Introducing Azure Service Bus Premium (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="9d4fd-182">Azure 服務匯流排進階簡介 (Channel9)</span><span class="sxs-lookup"><span data-stu-id="9d4fd-182">Introducing Azure Service Bus Premium (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="9d4fd-183">服務匯流排概觀</span><span class="sxs-lookup"><span data-stu-id="9d4fd-183">Service Bus overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="9d4fd-184">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="9d4fd-184">Azure Service Bus architecture overview</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="9d4fd-185">開始使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="9d4fd-185">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
