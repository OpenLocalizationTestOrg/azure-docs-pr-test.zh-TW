---
title: "aaaTransactions 和 Azure Service Fabric 可靠集合中的鎖定模式 |Microsoft 文件"
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
ms.openlocfilehash: 340e029aa98f43ad6e46b48f687dad01f9d96f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-and-lock-modes-in-azure-service-fabric-reliable-collections"></a><span data-ttu-id="3fdf3-103">Azure Service Fabric Reliable Collections 中的交易和鎖定模式</span><span class="sxs-lookup"><span data-stu-id="3fdf3-103">Transactions and lock modes in Azure Service Fabric Reliable Collections</span></span>

## <a name="transaction"></a><span data-ttu-id="3fdf3-104">交易</span><span class="sxs-lookup"><span data-stu-id="3fdf3-104">Transaction</span></span>
<span data-ttu-id="3fdf3-105">交易就是以單一工作邏輯單元執行的一連串作業。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-105">A transaction is a sequence of operations performed as a single logical unit of work.</span></span>
<span data-ttu-id="3fdf3-106">交易必須呈現出 hello 下列 ACID 屬性。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-106">A transaction must exhibit hello following ACID properties.</span></span> <span data-ttu-id="3fdf3-107">(請參閱：https://technet.microsoft.com/en-us/library/ms190612)</span><span class="sxs-lookup"><span data-stu-id="3fdf3-107">(see: https://technet.microsoft.com/en-us/library/ms190612)</span></span>
* <span data-ttu-id="3fdf3-108">**不可部分完成性**︰交易必須是不可部分完成的工作單位。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-108">**Atomicity**: A transaction must be an atomic unit of work.</span></span> <span data-ttu-id="3fdf3-109">換句話說，執行其所有資料修改，或完全不執行。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-109">In other words, either all its data modifications are performed, or none of them is performed.</span></span>
* <span data-ttu-id="3fdf3-110">**一致性**︰交易完成時，所有資料必須維持一致的狀態。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-110">**Consistency**: When completed, a transaction must leave all data in a consistent state.</span></span> <span data-ttu-id="3fdf3-111">所有的內部資料結構必須正確 hello hello 交易的結尾處。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-111">All internal data structures must be correct at hello end of hello transaction.</span></span>
* <span data-ttu-id="3fdf3-112">**隔離**： 並行的交易所做的修改都必須與其他並行的交易所做的 hello 修改。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-112">**Isolation**: Modifications made by concurrent transactions must be isolated from hello modifications made by any other concurrent transactions.</span></span> <span data-ttu-id="3fdf3-113">hello IReliableState 執行 hello 作業取決於用於作業中 itransaction:: hello 隔離等級。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-113">hello isolation level used for an operation within an ITransaction is determined by hello IReliableState performing hello operation.</span></span>
* <span data-ttu-id="3fdf3-114">**持久性**: 交易已完成之後，其作用便永遠就地 hello 系統中。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-114">**Durability**: After a transaction has completed, its effects are permanently in place in hello system.</span></span> <span data-ttu-id="3fdf3-115">hello 修改依然會保存即使在系統失敗的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-115">hello modifications persist even in hello event of a system failure.</span></span>

### <a name="isolation-levels"></a><span data-ttu-id="3fdf3-116">隔離層級</span><span class="sxs-lookup"><span data-stu-id="3fdf3-116">Isolation levels</span></span>
<span data-ttu-id="3fdf3-117">隔離等級定義 hello 程度 toowhich hello 交易必須是與其他交易所做的修改隔離。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-117">Isolation level defines hello degree toowhich hello transaction must be isolated from modifications made by other transactions.</span></span>
<span data-ttu-id="3fdf3-118">可靠的集合支援兩種隔離等級：</span><span class="sxs-lookup"><span data-stu-id="3fdf3-118">There are two isolation levels that are supported in Reliable Collections:</span></span>

* <span data-ttu-id="3fdf3-119">**可重複讀取**： 指定陳述式不能讀取已修改但尚未認可的其他交易的資料和任何其他交易可以修改已讀取的 hello 目前交易中，直到 hello 目前的資料交易完成。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-119">**Repeatable Read**: Specifies that statements cannot read data that has been modified but not yet committed by other transactions and that no other transactions can modify data that has been read by hello current transaction until hello current transaction finishes.</span></span> <span data-ttu-id="3fdf3-120">如需詳細資訊，請參閱 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-120">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>
* <span data-ttu-id="3fdf3-121">**快照集**： 指定在交易中任何陳述式所讀取的資料是 hello hello hello 交易開始時就存在的 hello 資料交易一致性版本。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-121">**Snapshot**: Specifies that data read by any statement in a transaction is hello transactionally consistent version of hello data that existed at hello start of hello transaction.</span></span>
  <span data-ttu-id="3fdf3-122">hello 交易可以辨識 hello hello 交易開始之前所認可的資料修改。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-122">hello transaction can recognize only data modifications that were committed before hello start of hello transaction.</span></span>
  <span data-ttu-id="3fdf3-123">Hello 開頭 hello 目前交易之後，其他交易所進行的資料修改將不會顯示 toostatements hello 目前交易中執行。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-123">Data modifications made by other transactions after hello start of hello current transaction are not visible toostatements executing in hello current transaction.</span></span>
  <span data-ttu-id="3fdf3-124">hello 效果是在交易中的 hello 陳述式會取得 hello 認可資料的快照集，存在於 hello hello 交易開始。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-124">hello effect is as if hello statements in a transaction get a snapshot of hello committed data as it existed at hello start of hello transaction.</span></span>
  <span data-ttu-id="3fdf3-125">可靠的集合的快照集都是一致的。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-125">Snapshots are consistent across Reliable Collections.</span></span>
  <span data-ttu-id="3fdf3-126">如需詳細資訊，請參閱 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-126">For more details, see [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx).</span></span>

<span data-ttu-id="3fdf3-127">可靠的集合會自動選擇 hello 隔離層級 toouse 交易的建立 hello 時根據 hello 作業和 hello hello 複本角色指定讀取作業。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-127">Reliable Collections automatically choose hello isolation level toouse for a given read operation depending on hello operation and hello role of hello replica at hello time of transaction's creation.</span></span>
<span data-ttu-id="3fdf3-128">以下是 hello 資料表，顯示隔離層級預設值為佇列和可靠的字典的作業。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-128">Following is hello table that depicts isolation level defaults for Reliable Dictionary and Queue operations.</span></span>

| <span data-ttu-id="3fdf3-129">作業 \ 角色</span><span class="sxs-lookup"><span data-stu-id="3fdf3-129">Operation \ Role</span></span> | <span data-ttu-id="3fdf3-130">主要</span><span class="sxs-lookup"><span data-stu-id="3fdf3-130">Primary</span></span> | <span data-ttu-id="3fdf3-131">次要</span><span class="sxs-lookup"><span data-stu-id="3fdf3-131">Secondary</span></span> |
| --- |:--- |:--- |
| <span data-ttu-id="3fdf3-132">單一實體讀取</span><span class="sxs-lookup"><span data-stu-id="3fdf3-132">Single Entity Read</span></span> |<span data-ttu-id="3fdf3-133">可重複讀取</span><span class="sxs-lookup"><span data-stu-id="3fdf3-133">Repeatable Read</span></span> |<span data-ttu-id="3fdf3-134">快照</span><span class="sxs-lookup"><span data-stu-id="3fdf3-134">Snapshot</span></span> |
| <span data-ttu-id="3fdf3-135">列舉、計數</span><span class="sxs-lookup"><span data-stu-id="3fdf3-135">Enumeration, Count</span></span> |<span data-ttu-id="3fdf3-136">快照</span><span class="sxs-lookup"><span data-stu-id="3fdf3-136">Snapshot</span></span> |<span data-ttu-id="3fdf3-137">快照</span><span class="sxs-lookup"><span data-stu-id="3fdf3-137">Snapshot</span></span> |

> [!NOTE]
> <span data-ttu-id="3fdf3-138">單一實體作業的常見範例包括 `IReliableDictionary.TryGetValueAsync`、`IReliableQueue.TryPeekAsync`。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-138">Common examples for Single Entity Operations are `IReliableDictionary.TryGetValueAsync`, `IReliableQueue.TryPeekAsync`.</span></span>
> 

<span data-ttu-id="3fdf3-139">Hello 可靠字典和 hello 可靠的佇列支援讀取程式寫入。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-139">Both hello Reliable Dictionary and hello Reliable Queue support Read Your Writes.</span></span>
<span data-ttu-id="3fdf3-140">換句話說，任何寫入交易內，就會看見 tooa 下列讀取的所屬 toohello 相同的交易。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-140">In other words, any write within a transaction will be visible tooa following read that belongs toohello same transaction.</span></span>

## <a name="locks"></a><span data-ttu-id="3fdf3-141">鎖定</span><span class="sxs-lookup"><span data-stu-id="3fdf3-141">Locks</span></span>
<span data-ttu-id="3fdf3-142">可靠的集合中使用嚴格的所有交易實作兩都階段鎖定： 交易不會釋放它所取得 hello 交易終止因中止或認可為止的 hello 鎖定。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-142">In Reliable Collections, all transactions implement rigorous two phase locking: a transaction does not release hello locks it has acquired until hello transaction terminates with either an abort or a commit.</span></span>

<span data-ttu-id="3fdf3-143">可靠的字典會針對所有單一實體作業使用資料列層級鎖定。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-143">Reliable Dictionary uses row level locking for all single entity operations.</span></span>
<span data-ttu-id="3fdf3-144">可靠的佇列則會針對嚴格交易的 FIFO 屬性交換並行。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-144">Reliable Queue trades off concurrency for strict transactional FIFO property.</span></span>
<span data-ttu-id="3fdf3-145">可靠的佇列會使用作業層級的鎖定，允許一次有 `TryPeekAsync` 和/或 `TryDequeueAsync` 的一個交易，以及有 `EnqueueAsync` 的一個交易。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-145">Reliable Queue uses operation level locks allowing one transaction with `TryPeekAsync` and/or `TryDequeueAsync` and one transaction with `EnqueueAsync` at a time.</span></span>
<span data-ttu-id="3fdf3-146">請注意該 toopreserve FIFO，如果`TryPeekAsync`或`TryDequeueAsync`曾經觀察的 hello 可靠的佇列是空的它們也會鎖定`EnqueueAsync`。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-146">Note that toopreserve FIFO, if a `TryPeekAsync` or `TryDequeueAsync` ever observes that hello Reliable Queue is empty, they will also lock `EnqueueAsync`.</span></span>

<span data-ttu-id="3fdf3-147">寫入作業一律會採取「獨佔」鎖定。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-147">Write operations always take Exclusive locks.</span></span>
<span data-ttu-id="3fdf3-148">對於讀取作業，hello 鎖定取決於一些因素。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-148">For read operations, hello locking depends on a couple of factors.</span></span>
<span data-ttu-id="3fdf3-149">任何使用快照隔離所完成的讀取作業都是無鎖定的。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-149">Any read operation done using Snapshot isolation is lock free.</span></span>
<span data-ttu-id="3fdf3-150">任何可重複讀取作業預設都會採用共用鎖定。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-150">Any Repeatable Read operation by default takes Shared locks.</span></span>
<span data-ttu-id="3fdf3-151">不過，支援可重複讀取的任何讀取作業，如 hello 使用者可以要求的更新鎖定，而不是 hello 共用鎖定。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-151">However, for any read operation that supports Repeatable Read, hello user can ask for an Update lock instead of hello Shared lock.</span></span>
<span data-ttu-id="3fdf3-152">更新鎖定是死結的對稱的鎖定使用 tooprevent 常見的多個交易鎖定資源並在稍後更新時所發生形式。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-152">An Update lock is an asymmetric lock used tooprevent a common form of deadlock that occurs when multiple transactions lock resources for potential updates at a later time.</span></span>

<span data-ttu-id="3fdf3-153">hello 下表中可以找到 hello 鎖定相容性矩陣：</span><span class="sxs-lookup"><span data-stu-id="3fdf3-153">hello lock compatibility matrix can be found in hello following table:</span></span>

| <span data-ttu-id="3fdf3-154">要求 \ 授與</span><span class="sxs-lookup"><span data-stu-id="3fdf3-154">Request \ Granted</span></span> | <span data-ttu-id="3fdf3-155">None</span><span class="sxs-lookup"><span data-stu-id="3fdf3-155">None</span></span> | <span data-ttu-id="3fdf3-156">共用</span><span class="sxs-lookup"><span data-stu-id="3fdf3-156">Shared</span></span> | <span data-ttu-id="3fdf3-157">更新</span><span class="sxs-lookup"><span data-stu-id="3fdf3-157">Update</span></span> | <span data-ttu-id="3fdf3-158">獨佔</span><span class="sxs-lookup"><span data-stu-id="3fdf3-158">Exclusive</span></span> |
| --- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="3fdf3-159">共用</span><span class="sxs-lookup"><span data-stu-id="3fdf3-159">Shared</span></span> |<span data-ttu-id="3fdf3-160">無衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-160">No conflict</span></span> |<span data-ttu-id="3fdf3-161">無衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-161">No conflict</span></span> |<span data-ttu-id="3fdf3-162">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-162">Conflict</span></span> |<span data-ttu-id="3fdf3-163">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-163">Conflict</span></span> |
| <span data-ttu-id="3fdf3-164">更新</span><span class="sxs-lookup"><span data-stu-id="3fdf3-164">Update</span></span> |<span data-ttu-id="3fdf3-165">無衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-165">No conflict</span></span> |<span data-ttu-id="3fdf3-166">無衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-166">No conflict</span></span> |<span data-ttu-id="3fdf3-167">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-167">Conflict</span></span> |<span data-ttu-id="3fdf3-168">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-168">Conflict</span></span> |
| <span data-ttu-id="3fdf3-169">獨佔</span><span class="sxs-lookup"><span data-stu-id="3fdf3-169">Exclusive</span></span> |<span data-ttu-id="3fdf3-170">無衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-170">No conflict</span></span> |<span data-ttu-id="3fdf3-171">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-171">Conflict</span></span> |<span data-ttu-id="3fdf3-172">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-172">Conflict</span></span> |<span data-ttu-id="3fdf3-173">衝突</span><span class="sxs-lookup"><span data-stu-id="3fdf3-173">Conflict</span></span> |

<span data-ttu-id="3fdf3-174">Hello 可靠集合的應用程式開發介面中的逾時引數用於死結偵測。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-174">Time-out argument in hello Reliable Collections APIs is used for deadlock detection.</span></span>
<span data-ttu-id="3fdf3-175">例如，兩筆交易 （T1 和 T2） 嘗試 tooread，並更新 K1。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-175">For example, two transactions (T1 and T2) are trying tooread and update K1.</span></span>
<span data-ttu-id="3fdf3-176">它有可能 toodeadlock，因為它們都得到擁有 hello 共用鎖定。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-176">It is possible for them toodeadlock, because they both end up having hello Shared lock.</span></span>
<span data-ttu-id="3fdf3-177">在此情況下，其中之一或兩者的 hello 作業會逾時。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-177">In this case, one or both of hello operations will time out.</span></span>

<span data-ttu-id="3fdf3-178">此死結案例就是更新鎖定可如何防止死結的絕佳範例。</span><span class="sxs-lookup"><span data-stu-id="3fdf3-178">This deadlock scenario is a great example of how an Update lock can prevent deadlocks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fdf3-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fdf3-179">Next steps</span></span>
* [<span data-ttu-id="3fdf3-180">使用可靠的集合</span><span class="sxs-lookup"><span data-stu-id="3fdf3-180">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="3fdf3-181">Reliable Services 通知</span><span class="sxs-lookup"><span data-stu-id="3fdf3-181">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="3fdf3-182">備份與還原 Reliable Services (災害復原)</span><span class="sxs-lookup"><span data-stu-id="3fdf3-182">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="3fdf3-183">Reliable State Manager 組態</span><span class="sxs-lookup"><span data-stu-id="3fdf3-183">Reliable State Manager configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="3fdf3-184">可靠的集合的開發人員參考資料</span><span class="sxs-lookup"><span data-stu-id="3fdf3-184">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

