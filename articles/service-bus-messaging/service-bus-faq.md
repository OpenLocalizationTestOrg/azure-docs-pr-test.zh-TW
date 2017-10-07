---
title: "aaaAzure Service Bus 常見問題集 (FAQ) |Microsoft 文件"
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
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a><span data-ttu-id="07438-103">服務匯流排常見問題集</span><span class="sxs-lookup"><span data-stu-id="07438-103">Service Bus FAQ</span></span>
<span data-ttu-id="07438-104">本文提供 Microsoft Azure 服務匯流排的一些常見問題解集。</span><span class="sxs-lookup"><span data-stu-id="07438-104">This article answers some frequently asked questions about Microsoft Azure Service Bus.</span></span> <span data-ttu-id="07438-105">您也可以造訪 hello [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)一般 Azure 定價和支援資訊。</span><span class="sxs-lookup"><span data-stu-id="07438-105">You can also visit hello [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span>

## <a name="general-questions-about-azure-service-bus"></a><span data-ttu-id="07438-106">關於 Azure 服務匯流排的一般問題</span><span class="sxs-lookup"><span data-stu-id="07438-106">General questions about Azure Service Bus</span></span>
### <a name="what-is-azure-service-bus"></a><span data-ttu-id="07438-107">什麼是 Azure 服務匯流排？</span><span class="sxs-lookup"><span data-stu-id="07438-107">What is Azure Service Bus?</span></span>
<span data-ttu-id="07438-108">[Azure 服務匯流排](service-bus-messaging-overview.md)是非同步傳訊雲端平台，可讓您 toosend 低耦合系統之間的資料。</span><span class="sxs-lookup"><span data-stu-id="07438-108">[Azure Service Bus](service-bus-messaging-overview.md) is an asynchronous messaging cloud platform that enables you toosend data between decoupled systems.</span></span> <span data-ttu-id="07438-109">Microsoft 提供此功能為服務時，這表示，您不需要 toohost 任一個順序 toouse 中硬體它。</span><span class="sxs-lookup"><span data-stu-id="07438-109">Microsoft offers this feature as a service, which means that you do not need toohost any of your own hardware in order toouse it.</span></span>

### <a name="what-is-a-service-bus-namespace"></a><span data-ttu-id="07438-110">什麼是服務匯流排命名空間？</span><span class="sxs-lookup"><span data-stu-id="07438-110">What is a Service Bus namespace?</span></span>
<span data-ttu-id="07438-111">[命名空間](service-bus-create-namespace-portal.md)提供範圍容器，可在應用程式內定址服務匯流排資源。</span><span class="sxs-lookup"><span data-stu-id="07438-111">A [namespace](service-bus-create-namespace-portal.md) provides a scoping container for addressing Service Bus resources within your application.</span></span> <span data-ttu-id="07438-112">建立一個必要 toouse Service Bus 並將會是其中一個 hello 中開始使用第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="07438-112">Creating one is necessary toouse Service Bus and will be one of hello first steps in getting started.</span></span>

### <a name="what-is-an-azure-service-bus-queue"></a><span data-ttu-id="07438-113">什麼是 Azure 服務匯流排佇列？</span><span class="sxs-lookup"><span data-stu-id="07438-113">What is an Azure Service Bus queue?</span></span>
<span data-ttu-id="07438-114">[服務匯流排佇列](service-bus-queues-topics-subscriptions.md)是訊息儲存所在的實體。</span><span class="sxs-lookup"><span data-stu-id="07438-114">A [Service Bus queue](service-bus-queues-topics-subscriptions.md) is an entity in which messages are stored.</span></span> <span data-ttu-id="07438-115">您有多個應用程式或需要 toocommunicate 彼此的分散式應用程式的多個部分時，佇列會特別有用。</span><span class="sxs-lookup"><span data-stu-id="07438-115">Queues are particularly useful when you have multiple applications, or multiple parts of a distributed application that need toocommunicate with each other.</span></span> <span data-ttu-id="07438-116">hello 佇列就類似 tooa 配送中心，也就是說，在接收或然後從該位置傳送多個產品 （訊息）。</span><span class="sxs-lookup"><span data-stu-id="07438-116">hello queue is similar tooa distribution center in that multiple products (messages) are received and then sent from that location.</span></span>

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a><span data-ttu-id="07438-117">什麼是 Azure 服務匯流排主題和訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="07438-117">What are Azure Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="07438-118">主題可視覺化為佇列，而且在使用多個訂用帳戶時，主題會變成更豐富的訊息模型；基本上是一對多的通訊工具。</span><span class="sxs-lookup"><span data-stu-id="07438-118">A topic can be visualized as a queue and when using multiple subscriptions, it becomes a richer messaging model; essentially a one-to-many communication tool.</span></span> <span data-ttu-id="07438-119">這個發行/訂閱模型 (或*pub/sub*) 可讓多個應用程式所接收該訊息會傳送具有多個訂用帳戶 toohave 訊息 tooa 主題的應用程式。</span><span class="sxs-lookup"><span data-stu-id="07438-119">This publish/subscribe model (or *pub/sub*) enables an application that sends a message tooa topic with multiple subscriptions toohave that message received by multiple applications.</span></span>

### <a name="what-is-a-partitioned-entity"></a><span data-ttu-id="07438-120">什麼是分割的實體？</span><span class="sxs-lookup"><span data-stu-id="07438-120">What is a partitioned entity?</span></span>
<span data-ttu-id="07438-121">傳統的佇列或主題由單一訊息代理程式處理並儲存在一個訊息存放區中。</span><span class="sxs-lookup"><span data-stu-id="07438-121">A conventional queue or topic is handled by a single message broker and stored in one messaging store.</span></span> <span data-ttu-id="07438-122">[分割的佇列或主題](service-bus-partitioning.md)會由多個訊息代理程式處理，並儲存在多個訊息存放區。</span><span class="sxs-lookup"><span data-stu-id="07438-122">A [partitioned queue or topic](service-bus-partitioning.md) is handled by multiple message brokers and stored in multiple messaging stores.</span></span> <span data-ttu-id="07438-123">這表示 hello 分割的佇列或主題的整體輸送量不再受限於單一訊息代理程式或訊息存放區的 hello 效能。</span><span class="sxs-lookup"><span data-stu-id="07438-123">This means that hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="07438-124">此外，即使訊息存放區暫時中斷也不會讓分割的佇列或主題無法使用。</span><span class="sxs-lookup"><span data-stu-id="07438-124">In addition, a temporary outage of a messaging store does not render a partitioned queue or topic unavailable.</span></span>

<span data-ttu-id="07438-125">請注意，使用分割實體時無法確保順序。</span><span class="sxs-lookup"><span data-stu-id="07438-125">Note that ordering is not ensured when using partitioning entities.</span></span> <span data-ttu-id="07438-126">在 hello 事件中的資料分割，就無法使用，您仍然可以傳送和接收來自 hello 其他資料分割的訊息。</span><span class="sxs-lookup"><span data-stu-id="07438-126">In hello event that a partition is unavailable, you can still send and receive messages from hello other partitions.</span></span>

## <a name="best-practices"></a><span data-ttu-id="07438-127">最佳作法</span><span class="sxs-lookup"><span data-stu-id="07438-127">Best practices</span></span>
### <a name="what-are-some-azure-service-bus-best-practices"></a><span data-ttu-id="07438-128">Azure 服務匯流排的最佳做法有哪些？</span><span class="sxs-lookup"><span data-stu-id="07438-128">What are some Azure Service Bus best practices?</span></span>
* <span data-ttu-id="07438-129">[使用服務匯流排的效能改進的最佳做法][ Best practices for performance improvements using Service Bus] – 這篇文章描述 toooptimize 效能交換時的訊息。</span><span class="sxs-lookup"><span data-stu-id="07438-129">[Best practices for performance improvements using Service Bus][Best practices for performance improvements using Service Bus] – this article describes how toooptimize performance when exchanging messages.</span></span>

### <a name="what-should-i-know-before-creating-entities"></a><span data-ttu-id="07438-130">建立實體前的須知事項為何？</span><span class="sxs-lookup"><span data-stu-id="07438-130">What should I know before creating entities?</span></span>
<span data-ttu-id="07438-131">下列屬性的佇列和主題的 hello 是不變。</span><span class="sxs-lookup"><span data-stu-id="07438-131">hello following properties of a queue and topic are immutable.</span></span> <span data-ttu-id="07438-132">在佈建實體時請將這一點納入考量，因為若要修改屬性，就必須建立新的替代實體。</span><span class="sxs-lookup"><span data-stu-id="07438-132">Please take this into account when you provision your entities as this cannot be modified, without creating a new replacement entity.</span></span>

* <span data-ttu-id="07438-133">大小</span><span class="sxs-lookup"><span data-stu-id="07438-133">Size</span></span>
* <span data-ttu-id="07438-134">分割</span><span class="sxs-lookup"><span data-stu-id="07438-134">Partitioning</span></span>
* <span data-ttu-id="07438-135">工作階段</span><span class="sxs-lookup"><span data-stu-id="07438-135">Sessions</span></span>
* <span data-ttu-id="07438-136">重複偵測</span><span class="sxs-lookup"><span data-stu-id="07438-136">Duplicate detection</span></span>
* <span data-ttu-id="07438-137">快速實體</span><span class="sxs-lookup"><span data-stu-id="07438-137">Express entity</span></span>

## <a name="pricing"></a><span data-ttu-id="07438-138">價格</span><span class="sxs-lookup"><span data-stu-id="07438-138">Pricing</span></span>
<span data-ttu-id="07438-139">本節將回答一些常見問題集疑問 hello 服務匯流排定價結構。</span><span class="sxs-lookup"><span data-stu-id="07438-139">This section answers some frequently-asked questions about hello Service Bus pricing structure.</span></span>

<span data-ttu-id="07438-140">hello[服務匯流排定價和計費](service-bus-pricing-billing.md)篇文章說明 hello 計費公尺，服務匯流排，而且服務匯流排定價選項的相關資訊，請參閱[服務匯流排定價詳細資料](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="07438-140">hello [Service Bus pricing and billing](service-bus-pricing-billing.md) article explains hello billing meters in Service Bus, and for information about Service Bus pricing options, see [Service Bus pricing details](https://azure.microsoft.com/pricing/details/service-bus/).</span></span>

<span data-ttu-id="07438-141">您也可以造訪 hello [Azure 支援常見問題集](http://go.microsoft.com/fwlink/?LinkID=185083)一般 azure 定價資訊。</span><span class="sxs-lookup"><span data-stu-id="07438-141">You can also visit hello [Azure Support FAQs](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing information.</span></span> 

### <a name="how-do-you-charge-for-service-bus"></a><span data-ttu-id="07438-142">服務匯流排的收費方式為何？</span><span class="sxs-lookup"><span data-stu-id="07438-142">How do you charge for Service Bus?</span></span>
<span data-ttu-id="07438-143">如需服務匯流排價格的完整資訊，請參閱[服務匯流排價格詳細資料][Pricing overview]。</span><span class="sxs-lookup"><span data-stu-id="07438-143">For complete information about Service Bus pricing, please see [Service Bus pricing details][Pricing overview].</span></span> <span data-ttu-id="07438-144">此外 toohello 價格所述，您必須支付 hello 佈建您的應用程式的資料中心外部輸出的相關聯的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="07438-144">In addition toohello prices noted, you are charged for associated data transfers for egress outside of hello data center in which your application is provisioned.</span></span>

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a><span data-ttu-id="07438-145">哪些 Service Bus 的使用會主旨 toodata 傳輸？</span><span class="sxs-lookup"><span data-stu-id="07438-145">What usage of Service Bus is subject toodata transfer?</span></span> <span data-ttu-id="07438-146">何種不需？</span><span class="sxs-lookup"><span data-stu-id="07438-146">What is not?</span></span>
<span data-ttu-id="07438-147">指定的 Azure 區域內的任何資料傳輸都是免費提供，以及任何輸入的資料傳輸。</span><span class="sxs-lookup"><span data-stu-id="07438-147">Any data transfer within a given Azure region is provided at no charge, as well as any inbound data transfer.</span></span> <span data-ttu-id="07438-148">位於區域外部的資料傳輸是可以找到主旨 tooegress 費用[這裡](https://azure.microsoft.com/pricing/details/bandwidth/)。</span><span class="sxs-lookup"><span data-stu-id="07438-148">Data transfer outside a region is subject tooegress charges which can be found [here](https://azure.microsoft.com/pricing/details/bandwidth/).</span></span>

### <a name="does-service-bus-charge-for-storage"></a><span data-ttu-id="07438-149">服務匯流排是否會收取儲存體費用？</span><span class="sxs-lookup"><span data-stu-id="07438-149">Does Service Bus charge for storage?</span></span>
<span data-ttu-id="07438-150">不會，服務匯流排不會收取儲存體費用。</span><span class="sxs-lookup"><span data-stu-id="07438-150">No, Service Bus does not charge for storage.</span></span> <span data-ttu-id="07438-151">不過，沒有配額限制 hello 最大資料量可以保存每個佇列/主題。</span><span class="sxs-lookup"><span data-stu-id="07438-151">However, there is a quota limiting hello maximum amount of data that can be persisted per queue/topic.</span></span> <span data-ttu-id="07438-152">請參閱 hello 下一個常見問題集。</span><span class="sxs-lookup"><span data-stu-id="07438-152">See hello next FAQ.</span></span>

## <a name="quotas"></a><span data-ttu-id="07438-153">配額</span><span class="sxs-lookup"><span data-stu-id="07438-153">Quotas</span></span>

<span data-ttu-id="07438-154">如需服務匯流排限制和配額的清單，請參閱 hello [Service Bus 配額概觀][Quotas overview]。</span><span class="sxs-lookup"><span data-stu-id="07438-154">For a list of Service Bus limits and quotas, see hello [Service Bus quotas overview][Quotas overview].</span></span>

### <a name="does-service-bus-have-any-usage-quotas"></a><span data-ttu-id="07438-155">服務匯流排是否有任何使用量配額？</span><span class="sxs-lookup"><span data-stu-id="07438-155">Does Service Bus have any usage quotas?</span></span>
<span data-ttu-id="07438-156">根據預設，對於所有雲端服務，Microsoft 會設定針對所有客戶的訂用帳戶計算的彙總每月使用量配額。</span><span class="sxs-lookup"><span data-stu-id="07438-156">By default, for any cloud service Microsoft sets an aggregate monthly usage quota that is calculated across all of a customer's subscriptions.</span></span> <span data-ttu-id="07438-157">因為我們了解您的需求可能超過這些限制，請隨時連絡客戶服務部門，讓我們能夠了解您的需求並適當地調整這些限制。</span><span class="sxs-lookup"><span data-stu-id="07438-157">Because we understand that you may need more than these limits, please contact customer service at any time so that we can understand your needs and adjust these limits appropriately.</span></span> <span data-ttu-id="07438-158">服務匯流排的 hello 整體使用量配額是每個月的 5 億訊息。</span><span class="sxs-lookup"><span data-stu-id="07438-158">For Service Bus, hello aggregate usage quota is 5 billion messages per month.</span></span>

<span data-ttu-id="07438-159">我們都有保留 hello 右 toodisable 已超過其使用量配額是指定月份中的客戶帳戶，而我們將提供電子郵件通知，並採取任何動作之前請多嘗試 toocontact 客戶。</span><span class="sxs-lookup"><span data-stu-id="07438-159">While we do reserve hello right toodisable a customer account that has exceeded its usage quotas in a given month, we will provide e-mail notification and make multiple attempts toocontact a customer before taking any action.</span></span> <span data-ttu-id="07438-160">超過這些配額的客戶仍會負責超過 hello 配額的費用。</span><span class="sxs-lookup"><span data-stu-id="07438-160">Customers exceeding these quotas will still be responsible for charges that exceed hello quotas.</span></span>

<span data-ttu-id="07438-161">如同 Azure 上的其他服務，服務匯流排會強制執行一組特定的配額 tooensure 沒有資源使用公平。</span><span class="sxs-lookup"><span data-stu-id="07438-161">As with other services on Azure, Service Bus enforces a set of specific quotas tooensure that there is fair usage of resources.</span></span> <span data-ttu-id="07438-162">您可以在 hello 找到這些配額的詳細[Service Bus 配額概觀][Quotas overview]。</span><span class="sxs-lookup"><span data-stu-id="07438-162">You can find more details about these quotas in hello [Service Bus quotas overview][Quotas overview].</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="07438-163">疑難排解</span><span class="sxs-lookup"><span data-stu-id="07438-163">Troubleshooting</span></span>
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a><span data-ttu-id="07438-164">有哪些 Azure 服務匯流排 Api 以及其建議的動作所產生的 hello 例外狀況？</span><span class="sxs-lookup"><span data-stu-id="07438-164">What are some of hello exceptions generated by Azure Service Bus APIs and their suggested actions?</span></span>
<span data-ttu-id="07438-165">如需可能的服務匯流排例外狀況，請參閱[例外狀況概觀][Exceptions overview]。</span><span class="sxs-lookup"><span data-stu-id="07438-165">For a list of possible Service Bus exceptions, see [Exceptions overview][Exceptions overview].</span></span>

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a><span data-ttu-id="07438-166">什麼是共用存取簽章，何種語言可支援產生簽章？</span><span class="sxs-lookup"><span data-stu-id="07438-166">What is a Shared Access Signature and which languages support generating a signature?</span></span>
<span data-ttu-id="07438-167">共用存取簽章是以 SHA-256 安全雜湊或 URI 為基礎的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="07438-167">Shared Access Signatures are an authentication mechanism based on SHA – 256 secure hashes or URIs.</span></span> <span data-ttu-id="07438-168">如需有關資訊 toogenerate 自己節點、 PHP、 Java 和 C 中的簽章\#，請參閱 hello[共用存取簽章][ Shared Access Signatures]發行項。</span><span class="sxs-lookup"><span data-stu-id="07438-168">For information about how toogenerate your own signatures in Node, PHP, Java and C\#, see hello [Shared Access Signatures][Shared Access Signatures] article.</span></span>

## <a name="subscription-and-namespace-management"></a><span data-ttu-id="07438-169">訂用帳戶和命名空間管理</span><span class="sxs-lookup"><span data-stu-id="07438-169">Subscription and namespace management</span></span>
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a><span data-ttu-id="07438-170">我要如何移轉命名空間 tooanother Azure 訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="07438-170">How do I migrate a namespace tooanother Azure subscription?</span></span>

<span data-ttu-id="07438-171">您可以移動命名空間從一個 Azure 訂用帳戶 tooanother，使用任一 hello [Azure 入口網站](https://portal.azure.com)或 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="07438-171">You can move a namespace from one Azure subscription tooanother, using either hello [Azure portal](https://portal.azure.com) or PowerShell commands.</span></span> <span data-ttu-id="07438-172">在訂單 tooexecute hello 作業中，hello 命名空間必須已經使用。</span><span class="sxs-lookup"><span data-stu-id="07438-172">In order tooexecute hello operation, hello namespace must already be active.</span></span> <span data-ttu-id="07438-173">執行 hello 命令 hello 使用者必須是系統管理員，在這兩個 hello 來源上的，與目標訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07438-173">hello user executing hello commands must be an administrator on both hello source and target subscriptions.</span></span>

#### <a name="portal"></a><span data-ttu-id="07438-174">入口網站</span><span class="sxs-lookup"><span data-stu-id="07438-174">Portal</span></span>

<span data-ttu-id="07438-175">toouse hello Azure 入口網站 toomigrate Service Bus 命名空間 tooanother 訂閱 hello 遵循[這裡](../azure-resource-manager/resource-group-move-resources.md#use-portal)。</span><span class="sxs-lookup"><span data-stu-id="07438-175">toouse hello Azure portal toomigrate Service Bus namespaces tooanother subscription, follow hello directions [here](../azure-resource-manager/resource-group-move-resources.md#use-portal).</span></span> 

#### <a name="powershell"></a><span data-ttu-id="07438-176">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07438-176">PowerShell</span></span>

<span data-ttu-id="07438-177">hello 以下 PowerShell 命令的順序會將命名空間從一個 Azure 訂用帳戶 tooanother。</span><span class="sxs-lookup"><span data-stu-id="07438-177">hello following sequence of PowerShell commands moves a namespace from one Azure subscription tooanother.</span></span> <span data-ttu-id="07438-178">tooexecute 這項作業，hello 命名空間必須已經是作用中，且執行 hello PowerShell 命令的 hello 使用者必須是這兩個 hello 來源與目標訂用帳戶的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="07438-178">tooexecute this operation, hello namespace must already be active, and hello user running hello PowerShell commands must be an administrator on both hello source and target subscriptions.</span></span>

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a><span data-ttu-id="07438-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07438-179">Next steps</span></span>
<span data-ttu-id="07438-180">toolearn 有關 Service Bus 的詳細資訊，請參閱下列主題中的 hello。</span><span class="sxs-lookup"><span data-stu-id="07438-180">toolearn more about Service Bus, see hello following topics.</span></span>

* [<span data-ttu-id="07438-181">Azure 服務匯流排進階簡介 (部落格文章)</span><span class="sxs-lookup"><span data-stu-id="07438-181">Introducing Azure Service Bus Premium (blog post)</span></span>](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [<span data-ttu-id="07438-182">Azure 服務匯流排進階簡介 (Channel9)</span><span class="sxs-lookup"><span data-stu-id="07438-182">Introducing Azure Service Bus Premium (Channel9)</span></span>](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [<span data-ttu-id="07438-183">服務匯流排概觀</span><span class="sxs-lookup"><span data-stu-id="07438-183">Service Bus overview</span></span>](service-bus-messaging-overview.md)
* [<span data-ttu-id="07438-184">Azure 服務匯流排架構概觀</span><span class="sxs-lookup"><span data-stu-id="07438-184">Azure Service Bus architecture overview</span></span>](service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="07438-185">開始使用服務匯流排佇列</span><span class="sxs-lookup"><span data-stu-id="07438-185">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
