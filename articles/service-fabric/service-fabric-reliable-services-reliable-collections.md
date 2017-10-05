---
title: "Azure Service Fabric 具狀態服務中的 Reliable Collection 簡介 | Microsoft Docs"
description: "Service Fabric 具狀態服務提供可靠的集合，可讓您撰寫高度可用、可調整且低延遲的雲端應用程式。"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: d0247ba0242af05ca6dcd8049ff9116683538fa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliable-collections-in-azure-service-fabric-stateful-services"></a><span data-ttu-id="ac6e7-103">Azure Service Fabric 具狀態服務中可靠的集合簡介</span><span class="sxs-lookup"><span data-stu-id="ac6e7-103">Introduction to Reliable Collections in Azure Service Fabric stateful services</span></span>
<span data-ttu-id="ac6e7-104">可靠的集合可讓您撰寫高度可用、可擴充且低延遲的雲端應用程式，如同您在撰寫單一電腦應用程式一般。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-104">Reliable Collections enable you to write highly available, scalable, and low-latency cloud applications as though you were writing single computer applications.</span></span> <span data-ttu-id="ac6e7-105">Microsoft.ServiceFabric.Data.Collections 命名空間中的類別提供一組集合，可讓您自動具有高度可用的狀態。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-105">The classes in the **Microsoft.ServiceFabric.Data.Collections** namespace provide a set of collections that automatically make your state highly available.</span></span> <span data-ttu-id="ac6e7-106">開發人員只需將程式設計為可靠的集合 API，並讓可靠的集合來管理複寫和本機狀態。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-106">Developers need to program only to the Reliable Collection APIs and let Reliable Collections manage the replicated and local state.</span></span>

<span data-ttu-id="ac6e7-107">可靠的集合和其他高可用性技術 (例如 Redis、Azure 表格服務和 Azure 佇列服務) 之間的主要差異是狀態會保留在本機服務執行個體中，但同時也被設定為高可用性。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-107">The key difference between Reliable Collections and other high-availability technologies (such as Redis, Azure Table service, and Azure Queue service) is that the state is kept locally in the service instance while also being made highly available.</span></span> <span data-ttu-id="ac6e7-108">這表示：</span><span class="sxs-lookup"><span data-stu-id="ac6e7-108">This means that:</span></span>

* <span data-ttu-id="ac6e7-109">所有讀取都在本機，可保障低延遲及高輸送量讀取。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-109">All reads are local, which results in low latency and high-throughput reads.</span></span>
* <span data-ttu-id="ac6e7-110">所有寫入都只會產生最少的網路 IO 數，可保障低延遲和高輸送量寫入。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-110">All writes incur the minimum number of network IOs, which results in low latency and high-throughput writes.</span></span>

![集合的演化圖。](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

<span data-ttu-id="ac6e7-112">我們可將可靠的集合視為 **System.Collections** 類別的自然進化：它們是一組新的集合，專為雲端和多電腦應用程式量身設計，且不會對開發人員提高複雜度。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-112">Reliable Collections can be thought of as the natural evolution of the **System.Collections** classes: a new set of collections that are designed for the cloud and multi-computer applications without increasing complexity for the developer.</span></span> <span data-ttu-id="ac6e7-113">因此，可靠的集合是：</span><span class="sxs-lookup"><span data-stu-id="ac6e7-113">As such, Reliable Collections are:</span></span>

* <span data-ttu-id="ac6e7-114">可複寫：進行狀態變更複寫以確保高可用性。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-114">Replicated: State changes are replicated for high availability.</span></span>
* <span data-ttu-id="ac6e7-115">可保存：資料會保存至磁碟，可在發生大規模中斷 (例如，資料中心停電) 時保障持續性。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-115">Persisted: Data is persisted to disk for durability against large-scale outages (for example, a datacenter power outage).</span></span>
* <span data-ttu-id="ac6e7-116">非同步：API 是非同步的，可確保在產生 IO 時不會封鎖執行緒。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-116">Asynchronous: APIs are asynchronous to ensure that threads are not blocked when incurring IO.</span></span>
* <span data-ttu-id="ac6e7-117">交易式：API 會利用交易的抽象方法，讓您能夠輕鬆管理服務內多個可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-117">Transactional: APIs utilize the abstraction of transactions so you can manage multiple Reliable Collections within a service easily.</span></span>

<span data-ttu-id="ac6e7-118">Reliable Collection 具有增強式一致性保證，可讓您更輕鬆地推論應用程式的狀態。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-118">Reliable Collections provide strong consistency guarantees out of the box to make reasoning about application state easier.</span></span>
<span data-ttu-id="ac6e7-119">增強式一致性的實現方式是藉由確保僅有在整個交易已記錄到複本多數仲裁之後 (包括主要複本)，才認可交易。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-119">Strong consistency is achieved by ensuring transaction commits finish only after the entire transaction has been logged on a majority quorum of replicas, including the primary.</span></span>
<span data-ttu-id="ac6e7-120">若要達成較弱的一致性，應用程式可在非同步認可傳回之前，返回向用戶端/要求者進行確認。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-120">To achieve weaker consistency, applications can acknowledge back to the client/requester before the asynchronous commit returns.</span></span>

<span data-ttu-id="ac6e7-121">可靠的集合 API 是並行集合 API (位於 **System.Collections.Concurrent** 命名空間) 的一種演化：</span><span class="sxs-lookup"><span data-stu-id="ac6e7-121">The Reliable Collections APIs are an evolution of concurrent collections APIs (found in the **System.Collections.Concurrent** namespace):</span></span>

* <span data-ttu-id="ac6e7-122">非同步：會傳回工作；不同於並行集合，其作業會受到複寫及保存。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-122">Asynchronous: Returns a task since, unlike concurrent collections, the operations are replicated and persisted.</span></span>
* <span data-ttu-id="ac6e7-123">沒有 out 參數：使用 `ConditionalValue<T>` 傳回 bool 和值，而不是 out 參數。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-123">No out parameters: Uses `ConditionalValue<T>` to return a bool and a value instead of out parameters.</span></span> <span data-ttu-id="ac6e7-124">`ConditionalValue<T>` 就像 `Nullable<T>`，但不需要 T 就可以成為結構。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-124">`ConditionalValue<T>` is like `Nullable<T>` but does not require T to be a struct.</span></span>
* <span data-ttu-id="ac6e7-125">交易：使用交易物件，讓使用者可在交易中的多個可靠的集合上群組動作。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-125">Transactions: Uses a transaction object to enable the user to group actions on multiple Reliable Collections in a transaction.</span></span>

<span data-ttu-id="ac6e7-126">現在，Microsoft.ServiceFabric.Data.Collections 包含三個集合：</span><span class="sxs-lookup"><span data-stu-id="ac6e7-126">Today, **Microsoft.ServiceFabric.Data.Collections** contains three collections:</span></span>

* <span data-ttu-id="ac6e7-127">[可靠的字典](https://msdn.microsoft.com/library/azure/dn971511.aspx)：表示可複寫、交易式和非同步索引鍵/值組的集合。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-127">[Reliable Dictionary](https://msdn.microsoft.com/library/azure/dn971511.aspx): Represents a replicated, transactional, and asynchronous collection of key/value pairs.</span></span> <span data-ttu-id="ac6e7-128">類似於 **ConcurrentDictionary**，其索引鍵和值可以是任何類型。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-128">Similar to **ConcurrentDictionary**, both the key and the value can be of any type.</span></span>
* <span data-ttu-id="ac6e7-129">[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)：表示可複寫、交易式和非同步的嚴格先進先出 (FIFO) 佇列。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-129">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx): Represents a replicated, transactional, and asynchronous strict first-in, first-out (FIFO) queue.</span></span> <span data-ttu-id="ac6e7-130">類似於 **ConcurrentQueue**，其值可以是任何類型。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-130">Similar to **ConcurrentQueue**, the value can be of any type.</span></span>
* <span data-ttu-id="ac6e7-131">[可靠的並行佇列](service-fabric-reliable-services-reliable-concurrent-queue.md)︰代表儘可能最佳的複寫、交易與非同步排序序列，以達到高輸送量。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-131">[Reliable Concurrent Queue](service-fabric-reliable-services-reliable-concurrent-queue.md): Represents a replicated, transactional, and asynchronous best effort ordering queue for high throughput.</span></span> <span data-ttu-id="ac6e7-132">類似於 ConcurrentQueue，其值可以是任何類型。</span><span class="sxs-lookup"><span data-stu-id="ac6e7-132">Similar to the **ConcurrentQueue**, the value can be of any type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac6e7-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ac6e7-133">Next steps</span></span>
* [<span data-ttu-id="ac6e7-134">Reliable Collection 指導方針與建議</span><span class="sxs-lookup"><span data-stu-id="ac6e7-134">Reliable Collection Guidelines & Recommendations</span></span>](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [<span data-ttu-id="ac6e7-135">使用 Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="ac6e7-135">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="ac6e7-136">交易和鎖定</span><span class="sxs-lookup"><span data-stu-id="ac6e7-136">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [<span data-ttu-id="ac6e7-137">Reliable State Manager 與 Collection 內部</span><span class="sxs-lookup"><span data-stu-id="ac6e7-137">Reliable State Manager and Collection Internals</span></span>](service-fabric-reliable-services-reliable-collections-internals.md)
* <span data-ttu-id="ac6e7-138">管理資料</span><span class="sxs-lookup"><span data-stu-id="ac6e7-138">Managing Data</span></span>
  * [<span data-ttu-id="ac6e7-139">備份與還原</span><span class="sxs-lookup"><span data-stu-id="ac6e7-139">Backup and Restore</span></span>](service-fabric-reliable-services-backup-restore.md)
  * [<span data-ttu-id="ac6e7-140">Notifications</span><span class="sxs-lookup"><span data-stu-id="ac6e7-140">Notifications</span></span>](service-fabric-reliable-services-notifications.md)
  * [<span data-ttu-id="ac6e7-141">可靠的集合序列化</span><span class="sxs-lookup"><span data-stu-id="ac6e7-141">Reliable Collection serialization</span></span>](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [<span data-ttu-id="ac6e7-142">序列化與升級</span><span class="sxs-lookup"><span data-stu-id="ac6e7-142">Serialization and Upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="ac6e7-143">Reliable State Manager 組態</span><span class="sxs-lookup"><span data-stu-id="ac6e7-143">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* <span data-ttu-id="ac6e7-144">其他</span><span class="sxs-lookup"><span data-stu-id="ac6e7-144">Others</span></span>
  * [<span data-ttu-id="ac6e7-145">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="ac6e7-145">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  * [<span data-ttu-id="ac6e7-146">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="ac6e7-146">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
