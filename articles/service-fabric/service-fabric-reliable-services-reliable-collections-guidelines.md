---
title: "aaaGuidelines （& s) 中 Azure Service Fabric 可靠集合的建議 |Microsoft 文件"
description: "使用 Service Fabric Reliable Collection 的指導方針與建議"
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
ms.date: 5/3/2017
ms.author: mcoskun
ms.openlocfilehash: bcdbc9d013bc044e06c43761e7f515c7e4bf340c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guidelines-and-recommendations-for-reliable-collections-in-azure-service-fabric"></a><span data-ttu-id="afc1e-103">Azure Service Fabric 中 Reliable Collection 的指導方針與建議</span><span class="sxs-lookup"><span data-stu-id="afc1e-103">Guidelines and recommendations for Reliable Collections in Azure Service Fabric</span></span>
<span data-ttu-id="afc1e-104">本節提供使用 Reliable State Manager 和 Reliable Collection 的指導方針。</span><span class="sxs-lookup"><span data-stu-id="afc1e-104">This section provides guidelines for using Reliable State Manager and Reliable Collections.</span></span> <span data-ttu-id="afc1e-105">hello 目標是避免常犯的錯誤 toohelp 使用者。</span><span class="sxs-lookup"><span data-stu-id="afc1e-105">hello goal is toohelp users avoid common pitfalls.</span></span>

<span data-ttu-id="afc1e-106">hello 指導方針會組織成簡單的建議前置詞與 hello 詞彙*不要*，*考慮*，*避免*和*不*。</span><span class="sxs-lookup"><span data-stu-id="afc1e-106">hello guidelines are organized as simple recommendations prefixed with hello terms *Do*, *Consider*, *Avoid* and *Do not*.</span></span>

* <span data-ttu-id="afc1e-107">請不要修改讀取作業所傳回自訂類型的物件 (例如 `TryPeekAsync` 或 `TryGetValueAsync`)。</span><span class="sxs-lookup"><span data-stu-id="afc1e-107">Do not modify an object of custom type returned by read operations (for example, `TryPeekAsync` or `TryGetValueAsync`).</span></span> <span data-ttu-id="afc1e-108">可靠的集合，就像並行的集合，傳回參考 toohello 物件並不是複本。</span><span class="sxs-lookup"><span data-stu-id="afc1e-108">Reliable Collections, just like Concurrent Collections, return a reference toohello objects and not a copy.</span></span>
* <span data-ttu-id="afc1e-109">不要再修改它傳回的自訂型別物件的深層複本 hello。</span><span class="sxs-lookup"><span data-stu-id="afc1e-109">Do deep copy hello returned object of a custom type before modifying it.</span></span> <span data-ttu-id="afc1e-110">由於結構和內建型別是由值傳遞，您不需要 toodo 在其上的深層複本。</span><span class="sxs-lookup"><span data-stu-id="afc1e-110">Since structs and built-in types are pass-by-value, you do not need toodo a deep copy on them.</span></span>
* <span data-ttu-id="afc1e-111">請不要針對逾時使用 `TimeSpan.MaxValue` 。</span><span class="sxs-lookup"><span data-stu-id="afc1e-111">Do not use `TimeSpan.MaxValue` for time-outs.</span></span> <span data-ttu-id="afc1e-112">逾時應該使用的 toodetect 死結。</span><span class="sxs-lookup"><span data-stu-id="afc1e-112">Time-outs should be used toodetect deadlocks.</span></span>
* <span data-ttu-id="afc1e-113">在認可、中止或處置交易之後，請勿使用該交易。</span><span class="sxs-lookup"><span data-stu-id="afc1e-113">Do not use a transaction after it has been committed, aborted, or disposed.</span></span>
* <span data-ttu-id="afc1e-114">不要 hello 其所建立的交易範圍外使用列舉型別。</span><span class="sxs-lookup"><span data-stu-id="afc1e-114">Do not use an enumeration outside of hello transaction scope it was created in.</span></span>
* <span data-ttu-id="afc1e-115">請不要在另一個交易的 `using` 陳述式內建立交易，因為它會造成死結。</span><span class="sxs-lookup"><span data-stu-id="afc1e-115">Do not create a transaction within another transaction’s `using` statement because it can cause deadlocks.</span></span>
* <span data-ttu-id="afc1e-116">務必確保 `IComparable<TKey>` 實作是正確的。</span><span class="sxs-lookup"><span data-stu-id="afc1e-116">Do ensure that your `IComparable<TKey>` implementation is correct.</span></span> <span data-ttu-id="afc1e-117">hello 系統，不需要相依性`IComparable<TKey>`合併檢查點和資料列。</span><span class="sxs-lookup"><span data-stu-id="afc1e-117">hello system takes dependency on `IComparable<TKey>` for merging checkpoints and rows.</span></span>
* <span data-ttu-id="afc1e-118">讀取意圖 tooupdate 的項目時，請勿使用更新鎖定它 tooprevent 特定類別的死結。</span><span class="sxs-lookup"><span data-stu-id="afc1e-118">Do use Update lock when reading an item with an intention tooupdate it tooprevent a certain class of deadlocks.</span></span>
* <span data-ttu-id="afc1e-119">請考慮您的項目 （例如，TKey + 可靠字典 Tvalue>） 80 Kb 以下： 更好的較小 hello。</span><span class="sxs-lookup"><span data-stu-id="afc1e-119">Consider keeping your items (for example, TKey + TValue for Reliable Dictionary) below 80 KBytes: smaller hello better.</span></span> <span data-ttu-id="afc1e-120">這會減少 hello 大型物件堆積使用量，以及磁碟和網路 IO 要求的數量。</span><span class="sxs-lookup"><span data-stu-id="afc1e-120">This reduces hello amount of Large Object Heap usage as well as disk and network IO requirements.</span></span> <span data-ttu-id="afc1e-121">通常，它可減少時只有一小部份 hello 值正在更新複寫重複的資料。</span><span class="sxs-lookup"><span data-stu-id="afc1e-121">Often, it reduces replicating duplicate data when only one small part of hello value is being updated.</span></span> <span data-ttu-id="afc1e-122">常見的方式 tooachieve 可靠字典中，這是第 toobreak 中的資料列 toomultiple 資料列。</span><span class="sxs-lookup"><span data-stu-id="afc1e-122">Common way tooachieve this in Reliable Dictionary, is toobreak your rows in toomultiple rows.</span></span>
* <span data-ttu-id="afc1e-123">請考慮使用備份和還原功能 toohave 災害復原。</span><span class="sxs-lookup"><span data-stu-id="afc1e-123">Consider using backup and restore functionality toohave disaster recovery.</span></span>
* <span data-ttu-id="afc1e-124">避免混用單一實體的作業和多實體作業 (例如`GetCountAsync`， `CreateEnumerableAsync`) hello 中相同的交易，因為 toohello 不同隔離等級。</span><span class="sxs-lookup"><span data-stu-id="afc1e-124">Avoid mixing single entity operations and multi-entity operations (e.g `GetCountAsync`, `CreateEnumerableAsync`) in hello same transaction due toohello different isolation levels.</span></span>
* <span data-ttu-id="afc1e-125">請務必處理 InvalidOperationException。</span><span class="sxs-lookup"><span data-stu-id="afc1e-125">Do handle InvalidOperationException.</span></span> <span data-ttu-id="afc1e-126">可以由各種原因而 hello 系統中止使用者交易。</span><span class="sxs-lookup"><span data-stu-id="afc1e-126">User transactions can be aborted by hello system for variety of reasons.</span></span> <span data-ttu-id="afc1e-127">比方說，當 hello 可靠狀態管理員已變更其主要角色或是長時間執行交易封鎖 hello 交易記錄截斷。</span><span class="sxs-lookup"><span data-stu-id="afc1e-127">For example, when hello Reliable State Manager is changing its role out of Primary or when a long-running transaction is blocking truncation of hello transactional log.</span></span> <span data-ttu-id="afc1e-128">在這種情況下，使用者可能會收到 InvalidOperationException，指出他們的交易已終止。</span><span class="sxs-lookup"><span data-stu-id="afc1e-128">In such cases, user may receive InvalidOperationException indicating that their transaction has already been terminated.</span></span> <span data-ttu-id="afc1e-129">假設，hello hello 交易終止並不會要求使用者 hello，最佳的方式 toohandle 這個例外狀況是 toodispose hello 交易，檢查是否已收到信號 hello 取消語彙基元 （或 hello hello 複本角色已變更），如果不建立新的交易並重試。</span><span class="sxs-lookup"><span data-stu-id="afc1e-129">Assuming, hello termination of hello transaction was not requested by hello user, best way toohandle this exception is toodispose hello transaction, check if hello cancellation token has been signaled (or hello role of hello replica has been changed), and if not create a new transaction and retry.</span></span>  

<span data-ttu-id="afc1e-130">以下是一些事情 tookeep 記住：</span><span class="sxs-lookup"><span data-stu-id="afc1e-130">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="afc1e-131">hello 預設逾時值為四個秒所有 hello 可靠集合的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="afc1e-131">hello default time-out is four seconds for all hello Reliable Collection APIs.</span></span> <span data-ttu-id="afc1e-132">大部分使用者應該使用 hello 預設逾時。</span><span class="sxs-lookup"><span data-stu-id="afc1e-132">Most users should use hello default time-out.</span></span>
* <span data-ttu-id="afc1e-133">hello 預設取消語彙基元是`CancellationToken.None`可靠 api 的集合。</span><span class="sxs-lookup"><span data-stu-id="afc1e-133">hello default cancellation token is `CancellationToken.None` in all Reliable Collections APIs.</span></span>
* <span data-ttu-id="afc1e-134">hello 索引鍵的型別參數 (*TKey*) 必須正確實作可靠的字典`GetHashCode()`和`Equals()`。</span><span class="sxs-lookup"><span data-stu-id="afc1e-134">hello key type parameter (*TKey*) for a Reliable Dictionary must correctly implement `GetHashCode()` and `Equals()`.</span></span> <span data-ttu-id="afc1e-135">索引鍵必須是不可變的。</span><span class="sxs-lookup"><span data-stu-id="afc1e-135">Keys must be immutable.</span></span>
* <span data-ttu-id="afc1e-136">tooachieve hello 可靠集合的高可用性，每個服務應該有至少一個目標和最小複本集大小為 3。</span><span class="sxs-lookup"><span data-stu-id="afc1e-136">tooachieve high availability for hello Reliable Collections, each service should have at least a target and minimum replica set size of 3.</span></span>
* <span data-ttu-id="afc1e-137">次要的 hello 的 「 讀取 」 操作可讀取不是仲裁認可的版本。</span><span class="sxs-lookup"><span data-stu-id="afc1e-137">Read operations on hello secondary may read versions that are not quorum committed.</span></span>
  <span data-ttu-id="afc1e-138">這表示從單一次要複本讀取的資料版本進度可能有誤。</span><span class="sxs-lookup"><span data-stu-id="afc1e-138">This means that a version of data that is read from a single secondary might be false progressed.</span></span>
  <span data-ttu-id="afc1e-139">從主要複本讀取一定最穩定︰進度一定不會有誤。</span><span class="sxs-lookup"><span data-stu-id="afc1e-139">Reads from Primary are always stable: can never be false progressed.</span></span>

### <a name="next-steps"></a><span data-ttu-id="afc1e-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="afc1e-140">Next steps</span></span>
* [<span data-ttu-id="afc1e-141">使用 Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="afc1e-141">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="afc1e-142">交易和鎖定</span><span class="sxs-lookup"><span data-stu-id="afc1e-142">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)
* [<span data-ttu-id="afc1e-143">Reliable State Manager 與 Collection 內部</span><span class="sxs-lookup"><span data-stu-id="afc1e-143">Reliable State Manager and Collection Internals</span></span>](service-fabric-reliable-services-reliable-collections-internals.md)
* <span data-ttu-id="afc1e-144">管理資料</span><span class="sxs-lookup"><span data-stu-id="afc1e-144">Managing Data</span></span>
  * [<span data-ttu-id="afc1e-145">備份與還原</span><span class="sxs-lookup"><span data-stu-id="afc1e-145">Backup and Restore</span></span>](service-fabric-reliable-services-backup-restore.md)
  * [<span data-ttu-id="afc1e-146">Notifications</span><span class="sxs-lookup"><span data-stu-id="afc1e-146">Notifications</span></span>](service-fabric-reliable-services-notifications.md)
  * [<span data-ttu-id="afc1e-147">序列化與升級</span><span class="sxs-lookup"><span data-stu-id="afc1e-147">Serialization and Upgrade</span></span>](service-fabric-application-upgrade-data-serialization.md)
  * [<span data-ttu-id="afc1e-148">Reliable State Manager 組態</span><span class="sxs-lookup"><span data-stu-id="afc1e-148">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* <span data-ttu-id="afc1e-149">其他</span><span class="sxs-lookup"><span data-stu-id="afc1e-149">Others</span></span>
  * [<span data-ttu-id="afc1e-150">Reliable Services 快速入門</span><span class="sxs-lookup"><span data-stu-id="afc1e-150">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
  * [<span data-ttu-id="afc1e-151">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="afc1e-151">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
