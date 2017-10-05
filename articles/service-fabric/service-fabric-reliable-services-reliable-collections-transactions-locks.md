---
title: "Azure Service Fabric Reliable Collections 中的交易和鎖定模式 | Microsoft Docs"
description: "Azure Service Fabric Reliable State Manager 和 Reliable Collections 交易和鎖定。"
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
ms.openlocfilehash: 3452473f5b2f86d29e46339c997193bc6403736a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a><span data-ttu-id="17ecd-103">Azure Service Fabric Reliable Collections 中的交易和鎖定模式</span><span class="sxs-lookup"><span data-stu-id="17ecd-103">Transactions and lock modes in Azure Service Fabric Reliable Collections</span></span>

## <a name="transaction"></a><span data-ttu-id="17ecd-104">交易</span><span class="sxs-lookup"><span data-stu-id="17ecd-104">Transaction</span></span>
<span data-ttu-id="17ecd-105">交易就是以單一工作邏輯單元執行的一連串作業。</span><span class="sxs-lookup"><span data-stu-id="17ecd-105">A transaction is a sequence of operations performed as a single logical unit of work.</span></span>
<span data-ttu-id="17ecd-106">交易必須顯現下列 ACID 屬性。</span><span class="sxs-lookup"><span data-stu-id="17ecd-106">A transaction must exhibit the following ACID properties.</span></span> <span data-ttu-id="17ecd-107">(請參閱：https://technet.microsoft.com/en-us/library/ms190612)</span><span class="sxs-lookup"><span data-stu-id="17ecd-107">(see: https://technet.microsoft.com/en-us/library/ms190612)</span></span>
* <span data-ttu-id="17ecd-108">**不可部分完成性**︰交易必須是不可部分完成的工作單位。</span><span class="sxs-lookup"><span data-stu-id="17ecd-108">**Atomicity**: A transaction must be an atomic unit of work.</span></span> <span data-ttu-id="17ecd-109">換句話說，執行其所有資料修改，或完全不執行。</span><span class="sxs-lookup"><span data-stu-id="17ecd-109">In other words, either all its data modifications are performed, or none of them is performed.</span></span>
* <span data-ttu-id="17ecd-110">**一致性**︰交易完成時，所有資料必須維持一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="17ecd-110">**Consistency**: When completed, a transaction must leave all data in a consistent state.</span></span> <span data-ttu-id="17ecd-111">所有內部資料結構在交易結束時必須是正確的。</span><span class="sxs-lookup"><span data-stu-id="17ecd-111">All internal data structures must be correct at the end of the transaction.</span></span>
* <span data-ttu-id="17ecd-112">**隔離**︰並行交易所做的修改，必須與任何其他並行交易所做的修改隔離。</span><span class="sxs-lookup"><span data-stu-id="17ecd-112">**Isolation**: Modifications made by concurrent transactions must be isolated from the modifications made by any other concurrent transactions.</span></span> <span data-ttu-id="17ecd-113">ITransaction 內的作業所用的隔離等級是由執行此作業的 IReliableState 所決定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-113">The isolation level used for an operation within an ITransaction is determined by the IReliableState performing the operation.</span></span>
* <span data-ttu-id="17ecd-114">**耐久性**：交易完成之後，其作用會永久存在系統中。</span><span class="sxs-lookup"><span data-stu-id="17ecd-114">**Durability**: After a transaction has completed, its effects are permanently in place in the system.</span></span> <span data-ttu-id="17ecd-115">即使發生系統失敗仍會保存修改。</span><span class="sxs-lookup"><span data-stu-id="17ecd-115">The modifications persist even in the event of a system failure.</span></span>

### <a name="isolation-levels"></a><span data-ttu-id="17ecd-116">隔離層級</span><span class="sxs-lookup"><span data-stu-id="17ecd-116">Isolation levels</span></span>
<span data-ttu-id="17ecd-117">隔離層級定義交易必須與其他交易所做的修改隔離的程度。</span><span class="sxs-lookup"><span data-stu-id="17ecd-117">Isolation level defines the degree to which the transaction must be isolated from modifications made by other transactions.</span></span>
<span data-ttu-id="17ecd-118">可靠的集合支援兩種隔離等級：</span><span class="sxs-lookup"><span data-stu-id="17ecd-118">There are two isolation levels that are supported in Reliable Collections:</span></span>

* <span data-ttu-id="17ecd-119">**可重複讀取**：指定陳述式無法讀取已經修改但尚未由其他交易確認的資料，以及指定在目前的交易完成之前，任何其他交易都不能修改已經由目前交易讀取的資料。</span><span class="sxs-lookup"><span data-stu-id="17ecd-119">**Repeatable Read**: Specifies that statements cannot read data that has been modified but not yet committed by other transactions and that no other transactions can modify data that has been read by the current transaction until the current transaction finishes.</span></span> <span data-ttu-id="17ecd-120">如需詳細資訊，請參閱 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。</span><span class="sxs-lookup"><span data-stu-id="17ecd-120">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>
* <span data-ttu-id="17ecd-121">**快照集**：指定交易中任何陳述式所讀取的資料都會與交易開始時就存在的資料版本一致。</span><span class="sxs-lookup"><span data-stu-id="17ecd-121">**Snapshot**: Specifies that data read by any statement in a transaction is the transactionally consistent version of the data that existed at the start of the transaction.</span></span>
  <span data-ttu-id="17ecd-122">交易只能辨識交易開始之前所認可的資料修改。</span><span class="sxs-lookup"><span data-stu-id="17ecd-122">The transaction can recognize only data modifications that were committed before the start of the transaction.</span></span>
  <span data-ttu-id="17ecd-123">在目前交易中執行的陳述式無法看到在目前交易開始之後，其他交易所進行的資料修改。</span><span class="sxs-lookup"><span data-stu-id="17ecd-123">Data modifications made by other transactions after the start of the current transaction are not visible to statements executing in the current transaction.</span></span>
  <span data-ttu-id="17ecd-124">效果就如同交易中的陳述式會取得認可資料的快照集，因為這項資料於交易開始時就存在。</span><span class="sxs-lookup"><span data-stu-id="17ecd-124">The effect is as if the statements in a transaction get a snapshot of the committed data as it existed at the start of the transaction.</span></span>
  <span data-ttu-id="17ecd-125">可靠的集合的快照集都是一致的。</span><span class="sxs-lookup"><span data-stu-id="17ecd-125">Snapshots are consistent across Reliable Collections.</span></span>
  <span data-ttu-id="17ecd-126">如需詳細資訊，請參閱 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。</span><span class="sxs-lookup"><span data-stu-id="17ecd-126">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>

<span data-ttu-id="17ecd-127">可靠的集合會依據交易建立時的作業和複本角色，自動選擇要用於指定讀取作業的隔離層級。</span><span class="sxs-lookup"><span data-stu-id="17ecd-127">Reliable Collections automatically choose the isolation level to use for a given read operation depending on the operation and the role of the replica at the time of transaction's creation.</span></span>
<span data-ttu-id="17ecd-128">下表說明可靠的字典和佇列作業的隔離等級預設值。</span><span class="sxs-lookup"><span data-stu-id="17ecd-128">Following is the table that depicts isolation level defaults for Reliable Dictionary and Queue operations.</span></span>

| <span data-ttu-id="17ecd-129">作業 \ 角色</span><span class="sxs-lookup"><span data-stu-id="17ecd-129">Operation \ Role</span></span> | <span data-ttu-id="17ecd-130">主要</span><span class="sxs-lookup"><span data-stu-id="17ecd-130">Primary</span></span> | <span data-ttu-id="17ecd-131">次要</span><span class="sxs-lookup"><span data-stu-id="17ecd-131">Secondary</span></span> |
| --- |:--- |:--- |
| <span data-ttu-id="17ecd-132">單一實體讀取</span><span class="sxs-lookup"><span data-stu-id="17ecd-132">Single Entity Read</span></span> |<span data-ttu-id="17ecd-133">可重複讀取</span><span class="sxs-lookup"><span data-stu-id="17ecd-133">Repeatable Read</span></span> |<span data-ttu-id="17ecd-134">快照</span><span class="sxs-lookup"><span data-stu-id="17ecd-134">Snapshot</span></span> |
| <span data-ttu-id="17ecd-135">列舉、計數</span><span class="sxs-lookup"><span data-stu-id="17ecd-135">Enumeration, Count</span></span> |<span data-ttu-id="17ecd-136">快照</span><span class="sxs-lookup"><span data-stu-id="17ecd-136">Snapshot</span></span> |<span data-ttu-id="17ecd-137">快照</span><span class="sxs-lookup"><span data-stu-id="17ecd-137">Snapshot</span></span> |

> [!NOTE]
> <span data-ttu-id="17ecd-138">單一實體作業的常見範例包括 `IReliableDictionary.TryGetValueAsync`、`IReliableQueue.TryPeekAsync`。</span><span class="sxs-lookup"><span data-stu-id="17ecd-138">Common examples for Single Entity Operations are `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.</span></span>
> 

<span data-ttu-id="17ecd-139">可靠的字典和可靠的佇列皆支援「讀寫一致性」(Read Your Writes)。</span><span class="sxs-lookup"><span data-stu-id="17ecd-139">Both the Reliable Dictionary and the Reliable Queue support Read Your Writes.</span></span>
<span data-ttu-id="17ecd-140">換句話說，在屬於相同交易的下列讀取作業皆可看到交易內的任何寫入作業。</span><span class="sxs-lookup"><span data-stu-id="17ecd-140">In other words, any write within a transaction will be visible to a following read that belongs to the same transaction.</span></span>

## <a name="locks"></a><span data-ttu-id="17ecd-141">鎖定</span><span class="sxs-lookup"><span data-stu-id="17ecd-141">Locks</span></span>
<span data-ttu-id="17ecd-142">在 Reliable Collections 中，所有交易都會實作嚴格的兩階段鎖定：在以中止或認可來終止交易之前，交易不會釋放它所取得的鎖定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-142">In Reliable Collections, all transactions implement rigorous two phase locking: a transaction does not release the locks it has acquired until the transaction terminates with either an abort or a commit.</span></span>

<span data-ttu-id="17ecd-143">可靠的字典會針對所有單一實體作業使用資料列層級鎖定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-143">Reliable Dictionary uses row level locking for all single entity operations.</span></span>
<span data-ttu-id="17ecd-144">可靠的佇列則會針對嚴格交易的 FIFO 屬性交換並行。</span><span class="sxs-lookup"><span data-stu-id="17ecd-144">Reliable Queue trades off concurrency for strict transactional FIFO property.</span></span>
<span data-ttu-id="17ecd-145">可靠的佇列會使用作業層級的鎖定，允許一次有 `TryPeekAsync` 和/或 `TryDequeueAsync` 的一個交易，以及有 `EnqueueAsync` 的一個交易。</span><span class="sxs-lookup"><span data-stu-id="17ecd-145">Reliable Queue uses operation level locks allowing one transaction with `TryPeekAsync` and/or `TryDequeueAsync` and one transaction with `EnqueueAsync` at a time.</span></span>
<span data-ttu-id="17ecd-146">請注意，為維持 FIFO，如果 `TryPeekAsync` 或 `TryDequeueAsync` 曾觀察到可靠的佇列是空的，則它們也會鎖定 `EnqueueAsync`。</span><span class="sxs-lookup"><span data-stu-id="17ecd-146">Note that to preserve FIFO, if a `TryPeekAsync` or `TryDequeueAsync` ever observes that the Reliable Queue is empty, they will also lock `EnqueueAsync`.</span></span>

<span data-ttu-id="17ecd-147">寫入作業一律會採取「獨佔」鎖定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-147">Write operations always take Exclusive locks.</span></span>
<span data-ttu-id="17ecd-148">讀取作業的鎖定則取決於一些因素。</span><span class="sxs-lookup"><span data-stu-id="17ecd-148">For read operations, the locking depends on a couple of factors.</span></span>
<span data-ttu-id="17ecd-149">任何使用快照隔離所完成的讀取作業都是無鎖定的。</span><span class="sxs-lookup"><span data-stu-id="17ecd-149">Any read operation done using Snapshot isolation is lock free.</span></span>
<span data-ttu-id="17ecd-150">任何可重複讀取作業預設都會採用共用鎖定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-150">Any Repeatable Read operation by default takes Shared locks.</span></span>
<span data-ttu-id="17ecd-151">不過，針對支援可重複讀取的任何讀取作業，使用者可以要求更新鎖定，而不是共用鎖定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-151">However, for any read operation that supports Repeatable Read, the user can ask for an Update lock instead of the Shared lock.</span></span>
<span data-ttu-id="17ecd-152">更新鎖定是一種非對稱式鎖定，用來避免常見的死結，這些死結通常會在多個交易鎖定資源稍後進行可能更新時發生。</span><span class="sxs-lookup"><span data-stu-id="17ecd-152">An Update lock is an asymmetric lock used to prevent a common form of deadlock that occurs when multiple transactions lock resources for potential updates at a later time.</span></span>

<span data-ttu-id="17ecd-153">下表中可找到鎖定相容性矩陣：</span><span class="sxs-lookup"><span data-stu-id="17ecd-153">The lock compatibility matrix can be found in the following table:</span></span>

| <span data-ttu-id="17ecd-154">要求 \ 授與</span><span class="sxs-lookup"><span data-stu-id="17ecd-154">Request \ Granted</span></span> | <span data-ttu-id="17ecd-155">None</span><span class="sxs-lookup"><span data-stu-id="17ecd-155">None</span></span> | <span data-ttu-id="17ecd-156">共用</span><span class="sxs-lookup"><span data-stu-id="17ecd-156">Shared</span></span> | <span data-ttu-id="17ecd-157">更新</span><span class="sxs-lookup"><span data-stu-id="17ecd-157">Update</span></span> | <span data-ttu-id="17ecd-158">獨佔</span><span class="sxs-lookup"><span data-stu-id="17ecd-158">Exclusive</span></span> |
| --- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="17ecd-159">共用</span><span class="sxs-lookup"><span data-stu-id="17ecd-159">Shared</span></span> |<span data-ttu-id="17ecd-160">無衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-160">No conflict</span></span> |<span data-ttu-id="17ecd-161">無衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-161">No conflict</span></span> |<span data-ttu-id="17ecd-162">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-162">Conflict</span></span> |<span data-ttu-id="17ecd-163">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-163">Conflict</span></span> |
| <span data-ttu-id="17ecd-164">更新</span><span class="sxs-lookup"><span data-stu-id="17ecd-164">Update</span></span> |<span data-ttu-id="17ecd-165">無衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-165">No conflict</span></span> |<span data-ttu-id="17ecd-166">無衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-166">No conflict</span></span> |<span data-ttu-id="17ecd-167">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-167">Conflict</span></span> |<span data-ttu-id="17ecd-168">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-168">Conflict</span></span> |
| <span data-ttu-id="17ecd-169">獨佔</span><span class="sxs-lookup"><span data-stu-id="17ecd-169">Exclusive</span></span> |<span data-ttu-id="17ecd-170">無衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-170">No conflict</span></span> |<span data-ttu-id="17ecd-171">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-171">Conflict</span></span> |<span data-ttu-id="17ecd-172">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-172">Conflict</span></span> |<span data-ttu-id="17ecd-173">衝突</span><span class="sxs-lookup"><span data-stu-id="17ecd-173">Conflict</span></span> |

<span data-ttu-id="17ecd-174">Reliable Collections API 中的逾時引數是用來進行死結偵測。</span><span class="sxs-lookup"><span data-stu-id="17ecd-174">Time-out argument in the Reliable Collections APIs is used for deadlock detection.</span></span>
<span data-ttu-id="17ecd-175">例如，有兩筆交易 (T1 和 T2) 嘗試讀取和更新 K1。</span><span class="sxs-lookup"><span data-stu-id="17ecd-175">For example, two transactions (T1 and T2) are trying to read and update K1.</span></span>
<span data-ttu-id="17ecd-176">這樣很可能會形成死結，因為它們最後都會有共用鎖定。</span><span class="sxs-lookup"><span data-stu-id="17ecd-176">It is possible for them to deadlock, because they both end up having the Shared lock.</span></span>
<span data-ttu-id="17ecd-177">在這種情況下，其中一個或兩個作業將會逾時。</span><span class="sxs-lookup"><span data-stu-id="17ecd-177">In this case, one or both of the operations will time out.</span></span>

<span data-ttu-id="17ecd-178">此死結案例就是更新鎖定可如何防止死結的絕佳範例。</span><span class="sxs-lookup"><span data-stu-id="17ecd-178">This deadlock scenario is a great example of how an Update lock can prevent deadlocks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17ecd-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17ecd-179">Next steps</span></span>
* [<span data-ttu-id="17ecd-180">使用可靠的集合</span><span class="sxs-lookup"><span data-stu-id="17ecd-180">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="17ecd-181">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="17ecd-181">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="17ecd-182">備份與還原 Reliable Services (災害復原)</span><span class="sxs-lookup"><span data-stu-id="17ecd-182">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="17ecd-183">Reliable State Manager 組態</span><span class="sxs-lookup"><span data-stu-id="17ecd-183">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="17ecd-184">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="17ecd-184">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

