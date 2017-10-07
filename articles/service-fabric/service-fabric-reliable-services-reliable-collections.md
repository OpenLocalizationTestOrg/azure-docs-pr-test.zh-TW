---
title: "在 Azure Service Fabric 可設定狀態服務 aaaIntroduction tooReliable 集合 |Microsoft 文件"
description: "Service Fabric 可設定狀態服務可提供可靠的集合，可讓您 toowrite 高可用、 可擴充且低度延遲的雲端應用程式。"
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
ms.openlocfilehash: 9f67c48f13e8b91b84977e127e2545cbb9d9a158
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliable-collections-in-azure-service-fabric-stateful-services"></a><span data-ttu-id="3dcd1-103">在 Azure Service Fabric 可設定狀態服務簡介 tooReliable 集合</span><span class="sxs-lookup"><span data-stu-id="3dcd1-103">Introduction tooReliable Collections in Azure Service Fabric stateful services</span></span>
<span data-ttu-id="3dcd1-104">可靠的集合可讓您 toowrite 高可用、 可擴充且低度延遲的雲端應用程式就好像您在撰寫單一電腦的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-104">Reliable Collections enable you toowrite highly available, scalable, and low-latency cloud applications as though you were writing single computer applications.</span></span> <span data-ttu-id="3dcd1-105">hello 中 hello 類別**Microsoft.ServiceFabric.Data.Collections**命名空間提供一組自動讓您的狀態具有高可用性的集合。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-105">hello classes in hello **Microsoft.ServiceFabric.Data.Collections** namespace provide a set of collections that automatically make your state highly available.</span></span> <span data-ttu-id="3dcd1-106">開發人員需要 tooprogram 只有 toohello 可靠集合的應用程式開發介面，並讓可靠管理複寫的 hello 和本機狀態的集合。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-106">Developers need tooprogram only toohello Reliable Collection APIs and let Reliable Collections manage hello replicated and local state.</span></span>

<span data-ttu-id="3dcd1-107">hello 可靠的集合和其他高可用性的技術 （例如 Redis、 Azure 資料表服務和 Azure 佇列服務） 之間的主要差異是，hello 狀態就會保留在本機在 hello 服務執行個體時也要成為高可用性。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-107">hello key difference between Reliable Collections and other high-availability technologies (such as Redis, Azure Table service, and Azure Queue service) is that hello state is kept locally in hello service instance while also being made highly available.</span></span> <span data-ttu-id="3dcd1-108">這表示：</span><span class="sxs-lookup"><span data-stu-id="3dcd1-108">This means that:</span></span>

* <span data-ttu-id="3dcd1-109">所有讀取都在本機，可保障低延遲及高輸送量讀取。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-109">All reads are local, which results in low latency and high-throughput reads.</span></span>
* <span data-ttu-id="3dcd1-110">所有寫入都造成 hello 最小網路 Io 數目，會導致低度延遲及高輸送量寫入。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-110">All writes incur hello minimum number of network IOs, which results in low latency and high-throughput writes.</span></span>

![集合的演化圖。](media/service-fabric-reliable-services-reliable-collections/ReliableCollectionsEvolution.png)

<span data-ttu-id="3dcd1-112">可靠的集合可以視為 hello 自然演進而來的 hello **System.Collections**類別： 一組新的集合，而不會增加複雜度 hello 雲端和多部電腦的應用程式所設計hello 開發人員。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-112">Reliable Collections can be thought of as hello natural evolution of hello **System.Collections** classes: a new set of collections that are designed for hello cloud and multi-computer applications without increasing complexity for hello developer.</span></span> <span data-ttu-id="3dcd1-113">因此，可靠的集合是：</span><span class="sxs-lookup"><span data-stu-id="3dcd1-113">As such, Reliable Collections are:</span></span>

* <span data-ttu-id="3dcd1-114">可複寫：進行狀態變更複寫以確保高可用性。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-114">Replicated: State changes are replicated for high availability.</span></span>
* <span data-ttu-id="3dcd1-115">保存： 資料會保存的 toodisk 為持久性免於大規模中斷 （例如，資料中心停電）。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-115">Persisted: Data is persisted toodisk for durability against large-scale outages (for example, a datacenter power outage).</span></span>
* <span data-ttu-id="3dcd1-116">非同步： 應用程式開發介面會非同步 tooensure 產生 IO 時不會封鎖執行緒。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-116">Asynchronous: APIs are asynchronous tooensure that threads are not blocked when incurring IO.</span></span>
* <span data-ttu-id="3dcd1-117">因此您可以輕鬆地管理多個可靠的集合，在服務中異動： 應用程式開發介面利用 hello 抽象的交易。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-117">Transactional: APIs utilize hello abstraction of transactions so you can manage multiple Reliable Collections within a service easily.</span></span>

<span data-ttu-id="3dcd1-118">可靠的集合會提供強式一致性可確保超出 hello 方塊 toomake 思考更輕鬆的應用程式狀態。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-118">Reliable Collections provide strong consistency guarantees out of hello box toomake reasoning about application state easier.</span></span>
<span data-ttu-id="3dcd1-119">強式一致性是由確保的交易的認可完成 hello 整筆交易有登入的複本，包括 hello 主要多數仲裁之後，才完成。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-119">Strong consistency is achieved by ensuring transaction commits finish only after hello entire transaction has been logged on a majority quorum of replicas, including hello primary.</span></span>
<span data-ttu-id="3dcd1-120">tooachieve 較弱的一致性，應用程式可以了解後 toohello 用戶端要求者 hello 非同步認可傳回之前。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-120">tooachieve weaker consistency, applications can acknowledge back toohello client/requester before hello asynchronous commit returns.</span></span>

<span data-ttu-id="3dcd1-121">hello 可靠集合 Api 是發展的並行集合應用程式開發介面 (位於 hello **System.Collections.Concurrent**命名空間):</span><span class="sxs-lookup"><span data-stu-id="3dcd1-121">hello Reliable Collections APIs are an evolution of concurrent collections APIs (found in hello **System.Collections.Concurrent** namespace):</span></span>

* <span data-ttu-id="3dcd1-122">因為不同於並行的集合，複寫和保存 hello operations 非同步： 傳回的工作。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-122">Asynchronous: Returns a task since, unlike concurrent collections, hello operations are replicated and persisted.</span></span>
* <span data-ttu-id="3dcd1-123">沒有 out 參數： 使用`ConditionalValue<T>`tooreturn bool 和而不是 out 參數的值。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-123">No out parameters: Uses `ConditionalValue<T>` tooreturn a bool and a value instead of out parameters.</span></span> <span data-ttu-id="3dcd1-124">`ConditionalValue<T>`就像`Nullable<T>`，但不需要 T toobe 結構。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-124">`ConditionalValue<T>` is like `Nullable<T>` but does not require T toobe a struct.</span></span>
* <span data-ttu-id="3dcd1-125">交易： 在交易中的多個可靠集合上使用交易物件 tooenable hello 使用者 toogroup 動作。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-125">Transactions: Uses a transaction object tooenable hello user toogroup actions on multiple Reliable Collections in a transaction.</span></span>

<span data-ttu-id="3dcd1-126">現在，Microsoft.ServiceFabric.Data.Collections 包含三個集合：</span><span class="sxs-lookup"><span data-stu-id="3dcd1-126">Today, **Microsoft.ServiceFabric.Data.Collections** contains three collections:</span></span>

* <span data-ttu-id="3dcd1-127">[可靠的字典](https://msdn.microsoft.com/library/azure/dn971511.aspx)：表示可複寫、交易式和非同步索引鍵/值組的集合。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-127">[Reliable Dictionary](https://msdn.microsoft.com/library/azure/dn971511.aspx): Represents a replicated, transactional, and asynchronous collection of key/value pairs.</span></span> <span data-ttu-id="3dcd1-128">類似太**ConcurrentDictionary**、 兩者 hello 索引鍵和 hello 值可以是任何類型。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-128">Similar too**ConcurrentDictionary**, both hello key and hello value can be of any type.</span></span>
* <span data-ttu-id="3dcd1-129">[可靠的佇列](https://msdn.microsoft.com/library/azure/dn971527.aspx)：表示可複寫、交易式和非同步的嚴格先進先出 (FIFO) 佇列。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-129">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx): Represents a replicated, transactional, and asynchronous strict first-in, first-out (FIFO) queue.</span></span> <span data-ttu-id="3dcd1-130">類似太**ConcurrentQueue**，hello 值可以是任何類型。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-130">Similar too**ConcurrentQueue**, hello value can be of any type.</span></span>
* <span data-ttu-id="3dcd1-131">[可靠的並行佇列](service-fabric-reliable-services-reliable-concurrent-queue.md)︰代表儘可能最佳的複寫、交易與非同步排序序列，以達到高輸送量。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-131">[Reliable Concurrent Queue](service-fabric-reliable-services-reliable-concurrent-queue.md): Represents a replicated, transactional, and asynchronous best effort ordering queue for high throughput.</span></span> <span data-ttu-id="3dcd1-132">類似 toohello **ConcurrentQueue**，hello 值可以是任何類型。</span><span class="sxs-lookup"><span data-stu-id="3dcd1-132">Similar toohello **ConcurrentQueue**, hello value can be of any type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dcd1-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3dcd1-133">Next steps</span></span>
* [<span data-ttu-id="3dcd1-134">Reliable Collection 指導方針與建議</span><span class="sxs-lookup"><span data-stu-id="3dcd1-134">Reliable Collection Guidelines & Recommendations</span></span>](service-fabric-reliable-services-reliable-collections-guidelines.md)
* [<span data-ttu-id="3dcd1-135">使用 Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="3dcd1-135">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="3dcd1-136">交易和鎖定</span><span class="sxs-lookup"><span data-stu-id="3dcd1-136">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [<span data-ttu-id="3dcd1-137">Reliable State Manager 與 Collection 內部</span><span class="sxs-lookup"><span data-stu-id="3dcd1-137">Reliable State Manager and Collection Internals</span></span>](service-fabric-reliable-services-reliable-collections-internals.md)
* <span data-ttu-id="3dcd1-138">管理資料</span><span class="sxs-lookup"><span data-stu-id="3dcd1-138">Managing Data</span></span>
  * [<span data-ttu-id="3dcd1-139">備份與還原</span><span class="sxs-lookup"><span data-stu-id="3dcd1-139">Backup and Restore</span></span>](service-fabric-reliable-services-backup-restore.md)
  * [<span data-ttu-id="3dcd1-140">Notifications</span><span class="sxs-lookup"><span data-stu-id="3dcd1-140">Notifications</span></span>](service-fabric-reliable-services-notifications.md)
  * [<span data-ttu-id="3dcd1-141">可靠的集合序列化</span><span class="sxs-lookup"><span data-stu-id="3dcd1-141">Reliable Collection serialization</span></span>](service-fabric-reliable-services-reliable-collections-serialization.md)
  * [<span data-ttu-id="3dcd1-142">序列化與升級</span><span class="sxs-lookup"><span data-stu-id="3dcd1-142">Serialization and Upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="3dcd1-143">Reliable State Manager 組態</span><span class="sxs-lookup"><span data-stu-id="3dcd1-143">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* <span data-ttu-id="3dcd1-144">其他</span><span class="sxs-lookup"><span data-stu-id="3dcd1-144">Others</span></span>
  * [<span data-ttu-id="3dcd1-145">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="3dcd1-145">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  * [<span data-ttu-id="3dcd1-146">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="3dcd1-146">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
