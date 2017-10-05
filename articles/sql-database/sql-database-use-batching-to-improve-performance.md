---
title: "如何使用批次處理來改善 Azure SQL Database 應用程式效能"
description: "本主題提供證據，表明批次處理資料庫作業可大幅改善 Azure SQL Database 應用程式的速度和延展性。 雖然這些批次處理技術適用於任何 SQL Server 資料庫，但本文的重點在於 Azure。"
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 22cff47444306e599325ba3035d83a0266d69c72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-batching-to-improve-sql-database-application-performance"></a><span data-ttu-id="7a11f-104">如何使用批次處理來改善 SQL Database 應用程式效能</span><span class="sxs-lookup"><span data-stu-id="7a11f-104">How to use batching to improve SQL Database application performance</span></span>
<span data-ttu-id="7a11f-105">批次處理 Azure SQL Database 的作業可大幅改善應用程式的效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-105">Batching operations to Azure SQL Database significantly improves the performance and scalability of your applications.</span></span> <span data-ttu-id="7a11f-106">為了瞭解優點，本文的第一個部分涵蓋一些範例測試結果，其中比較 SQL Database 的循序和批次要求。</span><span class="sxs-lookup"><span data-stu-id="7a11f-106">In order to understand the benefits, the first part of this article covers some sample test results that compare sequential and batched requests to a SQL Database.</span></span> <span data-ttu-id="7a11f-107">本文其餘部分說明技術、案例和考量因素，協助您在 Azure 應用程式中順利使用批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-107">The remainder of the article shows the techniques, scenarios, and considerations to help you to use batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="7a11f-108">為什麼批次處理對 SQL Database 很重要？</span><span class="sxs-lookup"><span data-stu-id="7a11f-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="7a11f-109">眾所周知，批次處理遠端服務的呼叫是一項可提升效能和延展性的策略。</span><span class="sxs-lookup"><span data-stu-id="7a11f-109">Batching calls to a remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="7a11f-110">與遠端服務進行任何互動都有固定的成本，例如序列化、網路傳輸和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="7a11f-110">There are fixed processing costs to any interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="7a11f-111">將許多個別交易包裝成單一批次可將這些成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="7a11f-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="7a11f-112">本文中，我們將探討 SQL Database 的各種批次處理策略和案例。</span><span class="sxs-lookup"><span data-stu-id="7a11f-112">In this paper, we want to examine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="7a11f-113">雖然這些策略對於使用 SQL Server 的內部部署應用程式也很重要，但基於一些理由，必須特別討論在 SQL Database 中使用批次處理：</span><span class="sxs-lookup"><span data-stu-id="7a11f-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting the use of batching for SQL Database:</span></span>

* <span data-ttu-id="7a11f-114">存取 SQL Database 時網路延遲可能很嚴重，特別是從相同的 Microsoft Azure 資料中心外部存取 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7a11f-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside the same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="7a11f-115">SQL Database 的多租用戶特性表示資料存取層的效率與資料庫的整體延展性有密切關係。</span><span class="sxs-lookup"><span data-stu-id="7a11f-115">The multitenant characteristics of SQL Database means that the efficiency of the data access layer correlates to the overall scalability of the database.</span></span> <span data-ttu-id="7a11f-116">SQL Database 必須防止任何單一租用戶/使用者獨佔資料庫資源，而損害其他租用戶的權益。</span><span class="sxs-lookup"><span data-stu-id="7a11f-116">SQL Database must prevent any single tenant/user from monopolizing database resources to the detriment of other tenants.</span></span> <span data-ttu-id="7a11f-117">為了避免使用量超出預先定義的配額，SQL Database 可以減少輸送量，或以節流例外狀況做出回應。</span><span class="sxs-lookup"><span data-stu-id="7a11f-117">In response to usage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="7a11f-118">效率 (例如批次處理) 可讓您在達到這些限制之前，在 SQL Database 上完成更多工作。</span><span class="sxs-lookup"><span data-stu-id="7a11f-118">Efficiencies, such as batching, enable you to do more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="7a11f-119">在使用多個資料庫 (分區化) 的架構下，批次處理也很有效益。</span><span class="sxs-lookup"><span data-stu-id="7a11f-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="7a11f-120">就整體延展性而言，與每個資料庫單位的互動效率仍然是關鍵因素。</span><span class="sxs-lookup"><span data-stu-id="7a11f-120">The efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="7a11f-121">使用 SQL Database 的優點之一是您不必管理裝載著資料庫的伺服器。</span><span class="sxs-lookup"><span data-stu-id="7a11f-121">One of the benefits of using SQL Database is that you don’t have to manage the servers that host the database.</span></span> <span data-ttu-id="7a11f-122">不過，這種受管理的基礎結構也表示您必須以不同角度來思考資料庫最佳化。</span><span class="sxs-lookup"><span data-stu-id="7a11f-122">However, this managed infrastructure also means that you have to think differently about database optimizations.</span></span> <span data-ttu-id="7a11f-123">您不必再設法改善資料庫硬體或網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7a11f-123">You can no longer look to improve the database hardware or network infrastructure.</span></span> <span data-ttu-id="7a11f-124">Microsoft Azure 會控制那些環境。</span><span class="sxs-lookup"><span data-stu-id="7a11f-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="7a11f-125">您可以控制的主要方面是應用程式與 SQL Database 之間的互動方式。</span><span class="sxs-lookup"><span data-stu-id="7a11f-125">The main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="7a11f-126">批次處理屬於這些最佳化作法之一。</span><span class="sxs-lookup"><span data-stu-id="7a11f-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="7a11f-127">本文的第一個部分針對使用 SQL Database 的 .NET 應用程式，探討各種批次處理技術。</span><span class="sxs-lookup"><span data-stu-id="7a11f-127">The first part of the paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="7a11f-128">最後兩節涵蓋批次處理方針和案例。</span><span class="sxs-lookup"><span data-stu-id="7a11f-128">The last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="7a11f-129">批次處理策略</span><span class="sxs-lookup"><span data-stu-id="7a11f-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="7a11f-130">有關本主題中計時結果的注意事項</span><span class="sxs-lookup"><span data-stu-id="7a11f-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="7a11f-131">結果並不是基準，主要是示範 **相對效能**。</span><span class="sxs-lookup"><span data-stu-id="7a11f-131">Results are not benchmarks but are meant to show **relative performance**.</span></span> <span data-ttu-id="7a11f-132">計時至少根據 10 個測試回合的平均值。</span><span class="sxs-lookup"><span data-stu-id="7a11f-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="7a11f-133">作業插入至空的資料表。</span><span class="sxs-lookup"><span data-stu-id="7a11f-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="7a11f-134">這些測試是在 V12 以前的版本中測量，不見得符合您在 V12 資料庫中使用新的 [服務層](sql-database-service-tiers.md)時可能遇過的輸送量。</span><span class="sxs-lookup"><span data-stu-id="7a11f-134">These tests were measured pre-V12, and they do not necessarily correspond to throughput that you might experience in a V12 database using the new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="7a11f-135">批次處理技術的相對優點應該類似。</span><span class="sxs-lookup"><span data-stu-id="7a11f-135">The relative benefit of the batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="7a11f-136">交易</span><span class="sxs-lookup"><span data-stu-id="7a11f-136">Transactions</span></span>
<span data-ttu-id="7a11f-137">從討論交易來開始評論批次處理可能有點奇怪。</span><span class="sxs-lookup"><span data-stu-id="7a11f-137">It seems strange to begin a review of batching by discussing transactions.</span></span> <span data-ttu-id="7a11f-138">但使用用戶端交易也隱約有可改善效能的伺服器端批次處理效果。</span><span class="sxs-lookup"><span data-stu-id="7a11f-138">But the use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="7a11f-139">只需要幾行程式碼就能新增交易，因此可快速改善循序作業的效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-139">And transactions can be added with only a few lines of code, so they provide a fast way to improve performance of sequential operations.</span></span>

<span data-ttu-id="7a11f-140">請考慮下列 C# 程式碼，其中對一個簡易資料表執行一連串插入和更新作業。</span><span class="sxs-lookup"><span data-stu-id="7a11f-140">Consider the following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="7a11f-141">下列 ADO.NET 程式碼會循序執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="7a11f-141">The following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="7a11f-142">若要將這段程式碼最佳化，最佳方式是針對這些呼叫，實作某種形式的用戶端批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-142">The best way to optimize this code is to implement some form of client-side batching of these calls.</span></span> <span data-ttu-id="7a11f-143">還有更簡單的作法，只要將呼叫序列包裝在交易中，就能提升這段程式碼的效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-143">But there is a simple way to increase the performance of this code by simply wrapping the sequence of calls in a transaction.</span></span> <span data-ttu-id="7a11f-144">以下是使用交易的相同程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a11f-144">Here is the same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="7a11f-145">這兩個範例實際上都使用交易。</span><span class="sxs-lookup"><span data-stu-id="7a11f-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="7a11f-146">在第一個範例中，每個個別的呼叫就是隱含的交易。</span><span class="sxs-lookup"><span data-stu-id="7a11f-146">In the first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="7a11f-147">在第二個範例中，明確的交易包裝所有的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-147">In the second example, an explicit transaction wraps all of the calls.</span></span> <span data-ttu-id="7a11f-148">如 [預先寫入交易記錄](https://msdn.microsoft.com/library/ms186259.aspx)所述，交易認可時，記錄檔記錄會排清到磁碟。</span><span class="sxs-lookup"><span data-stu-id="7a11f-148">Per the documentation for the [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed to the disk when the transaction commits.</span></span> <span data-ttu-id="7a11f-149">因此，交易中包含越多呼叫，就越可能延遲到認可交易時，才會寫入交易記錄檔。</span><span class="sxs-lookup"><span data-stu-id="7a11f-149">So by including more calls in a transaction, the write to the transaction log can delay until the transaction is committed.</span></span> <span data-ttu-id="7a11f-150">事實上，您是對寫入伺服器交易記錄檔的動作啟用批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-150">In effect, you are enabling batching for the writes to the server’s transaction log.</span></span>

<span data-ttu-id="7a11f-151">下表顯示一些臨機操作測試結果。</span><span class="sxs-lookup"><span data-stu-id="7a11f-151">The following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="7a11f-152">這些測試分別以有交易和無交易，執行相同的循序插入。</span><span class="sxs-lookup"><span data-stu-id="7a11f-152">The tests performed the same sequential inserts with and without transactions.</span></span> <span data-ttu-id="7a11f-153">為了進一步觀察，第一組測試是從遠端的膝上型電腦連到 Microsoft Azure 中的資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="7a11f-153">For more perspective, the first set of tests ran remotely from a laptop to the database in Microsoft Azure.</span></span> <span data-ttu-id="7a11f-154">第二組測試是從位在相同 Microsoft Azure 資料中心 (美國西部) 內的雲端服務和資料庫執行。</span><span class="sxs-lookup"><span data-stu-id="7a11f-154">The second set of tests ran from a cloud service and database that both resided within the same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="7a11f-155">下表分別以有交易和無交易，顯示循序插入的持續時間 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-155">The following table shows the duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="7a11f-156">**內部部署至 Azure**：</span><span class="sxs-lookup"><span data-stu-id="7a11f-156">**On-Premises to Azure**:</span></span>

| <span data-ttu-id="7a11f-157">作業</span><span class="sxs-lookup"><span data-stu-id="7a11f-157">Operations</span></span> | <span data-ttu-id="7a11f-158">無交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-158">No Transaction (ms)</span></span> | <span data-ttu-id="7a11f-159">交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a11f-160">1</span><span class="sxs-lookup"><span data-stu-id="7a11f-160">1</span></span> |<span data-ttu-id="7a11f-161">130</span><span class="sxs-lookup"><span data-stu-id="7a11f-161">130</span></span> |<span data-ttu-id="7a11f-162">402</span><span class="sxs-lookup"><span data-stu-id="7a11f-162">402</span></span> |
| <span data-ttu-id="7a11f-163">10</span><span class="sxs-lookup"><span data-stu-id="7a11f-163">10</span></span> |<span data-ttu-id="7a11f-164">1208</span><span class="sxs-lookup"><span data-stu-id="7a11f-164">1208</span></span> |<span data-ttu-id="7a11f-165">1226</span><span class="sxs-lookup"><span data-stu-id="7a11f-165">1226</span></span> |
| <span data-ttu-id="7a11f-166">100</span><span class="sxs-lookup"><span data-stu-id="7a11f-166">100</span></span> |<span data-ttu-id="7a11f-167">12662</span><span class="sxs-lookup"><span data-stu-id="7a11f-167">12662</span></span> |<span data-ttu-id="7a11f-168">10395</span><span class="sxs-lookup"><span data-stu-id="7a11f-168">10395</span></span> |
| <span data-ttu-id="7a11f-169">1000</span><span class="sxs-lookup"><span data-stu-id="7a11f-169">1000</span></span> |<span data-ttu-id="7a11f-170">128852</span><span class="sxs-lookup"><span data-stu-id="7a11f-170">128852</span></span> |<span data-ttu-id="7a11f-171">102917</span><span class="sxs-lookup"><span data-stu-id="7a11f-171">102917</span></span> |

<span data-ttu-id="7a11f-172">**Azure 至 Azure (相同資料中心)**：</span><span class="sxs-lookup"><span data-stu-id="7a11f-172">**Azure to Azure (same datacenter)**:</span></span>

| <span data-ttu-id="7a11f-173">作業</span><span class="sxs-lookup"><span data-stu-id="7a11f-173">Operations</span></span> | <span data-ttu-id="7a11f-174">無交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-174">No Transaction (ms)</span></span> | <span data-ttu-id="7a11f-175">交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a11f-176">1</span><span class="sxs-lookup"><span data-stu-id="7a11f-176">1</span></span> |<span data-ttu-id="7a11f-177">21</span><span class="sxs-lookup"><span data-stu-id="7a11f-177">21</span></span> |<span data-ttu-id="7a11f-178">26</span><span class="sxs-lookup"><span data-stu-id="7a11f-178">26</span></span> |
| <span data-ttu-id="7a11f-179">10</span><span class="sxs-lookup"><span data-stu-id="7a11f-179">10</span></span> |<span data-ttu-id="7a11f-180">220</span><span class="sxs-lookup"><span data-stu-id="7a11f-180">220</span></span> |<span data-ttu-id="7a11f-181">56</span><span class="sxs-lookup"><span data-stu-id="7a11f-181">56</span></span> |
| <span data-ttu-id="7a11f-182">100</span><span class="sxs-lookup"><span data-stu-id="7a11f-182">100</span></span> |<span data-ttu-id="7a11f-183">2145</span><span class="sxs-lookup"><span data-stu-id="7a11f-183">2145</span></span> |<span data-ttu-id="7a11f-184">341</span><span class="sxs-lookup"><span data-stu-id="7a11f-184">341</span></span> |
| <span data-ttu-id="7a11f-185">1000</span><span class="sxs-lookup"><span data-stu-id="7a11f-185">1000</span></span> |<span data-ttu-id="7a11f-186">21479</span><span class="sxs-lookup"><span data-stu-id="7a11f-186">21479</span></span> |<span data-ttu-id="7a11f-187">2756</span><span class="sxs-lookup"><span data-stu-id="7a11f-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="7a11f-188">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="7a11f-188">Results are not benchmarks.</span></span> <span data-ttu-id="7a11f-189">請參閱 [有關本主題中計時結果的注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-189">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="7a11f-190">根據先前的測試結果，將單一作業包裝在交易中確實會降低效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-190">Based on the previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="7a11f-191">但隨著您增加單一交易內的作業數目，效能改善會變得越明顯。</span><span class="sxs-lookup"><span data-stu-id="7a11f-191">But as you increase the number of operations within a single transaction, the performance improvement becomes more marked.</span></span> <span data-ttu-id="7a11f-192">當所有作業都在 Microsoft Azure 資料中心內發生時，效能差異也會更明顯。</span><span class="sxs-lookup"><span data-stu-id="7a11f-192">The performance difference is also more noticeable when all operations occur within the Microsoft Azure datacenter.</span></span> <span data-ttu-id="7a11f-193">從 Microsoft Azure 資料中心外部使用 SQL Database 而增加的延遲，讓使用交易所提升的效能黯然失色。</span><span class="sxs-lookup"><span data-stu-id="7a11f-193">The increased latency of using SQL Database from outside the Microsoft Azure datacenter overshadows the performance gain of using transactions.</span></span>

<span data-ttu-id="7a11f-194">雖然使用交易可以提高效能，但要持續 [尋找交易和連接的最佳作法](https://msdn.microsoft.com/library/ms187484.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-194">Although the use of transactions can increase performance, continue to [observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="7a11f-195">交易儘可能越短越好，並於工作完成後立即關閉資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="7a11f-195">Keep the transaction as short as possible, and close the database connection after the work completes.</span></span> <span data-ttu-id="7a11f-196">使用上述範例中的陳述式可確保後續的程式碼區塊完成時關閉連接。</span><span class="sxs-lookup"><span data-stu-id="7a11f-196">The using statement in the previous example assures that the connection is closed when the subsequent code block completes.</span></span>

<span data-ttu-id="7a11f-197">上述範例示範只要使用兩行程式碼，就能將本機交易新增至任何 ADO.NET 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7a11f-197">The previous example demonstrates that you can add a local transaction to any ADO.NET code with two lines.</span></span> <span data-ttu-id="7a11f-198">對於執行循序插入、更新和刪除作業的程式碼，交易可以快速改善程式碼的效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-198">Transactions offer a quick way to improve the performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="7a11f-199">不過，若要達到最快效能，請考慮進一步變更程式碼來利用用戶端批次處理，例如資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-199">However, for the fastest performance, consider changing the code further to take advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="7a11f-200">如需 ADO.NET 中的交易的詳細資訊，請參閱 [ADO.NET 中的本機交易](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="7a11f-201">資料表值參數</span><span class="sxs-lookup"><span data-stu-id="7a11f-201">Table-valued parameters</span></span>
<span data-ttu-id="7a11f-202">資料表值參數支援使用者定義資料表類型做為 Transact-SQL 陳述式、預存程序和函數中的參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="7a11f-203">此用戶端批次處理技術可讓您在資料表值參數內傳送很多列的資料。</span><span class="sxs-lookup"><span data-stu-id="7a11f-203">This client-side batching technique allows you to send multiple rows of data within the table-valued parameter.</span></span> <span data-ttu-id="7a11f-204">若要使用資料表值參數，請先定義資料表類型。</span><span class="sxs-lookup"><span data-stu-id="7a11f-204">To use table-valued parameters, first define a table type.</span></span> <span data-ttu-id="7a11f-205">下列 Transact-SQL 陳述式會建立名為 **MyTableType**的資料表類型。</span><span class="sxs-lookup"><span data-stu-id="7a11f-205">The following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="7a11f-206">在程式碼中，您使用與此資料表類型完全相同的名稱和類型建立 **DataTable** 。</span><span class="sxs-lookup"><span data-stu-id="7a11f-206">In code, you create a **DataTable** with the exact same names and types of the table type.</span></span> <span data-ttu-id="7a11f-207">將這個 **DataTable** 傳入文字查詢或預存程序呼叫中的參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="7a11f-208">下列範例示範這項技巧：</span><span class="sxs-lookup"><span data-stu-id="7a11f-208">The following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. The following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="7a11f-209">在上述範例中，**SqlCommand** 物件從資料表值參數 **@TestTvp** 插入資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-209">In the previous example, the **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="7a11f-210">先前建立的 **DataTable** 物件透過 **SqlCommand.Parameters.Add** 方法指派給此參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-210">The previously created **DataTable** object is assigned to this parameter with the **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="7a11f-211">在一個呼叫中批次處理插入的效能明顯高於循序插入。</span><span class="sxs-lookup"><span data-stu-id="7a11f-211">Batching the inserts in one call significantly increases the performance over sequential inserts.</span></span>

<span data-ttu-id="7a11f-212">若要進一步改善上述範例，請使用預存程序代替文字式命令。</span><span class="sxs-lookup"><span data-stu-id="7a11f-212">To improve the previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="7a11f-213">下列 Transact-SQL 命令會建立一個接受 **SimpleTestTableType** 資料表值參數的預存程序。</span><span class="sxs-lookup"><span data-stu-id="7a11f-213">The following Transact-SQL command creates a stored procedure that takes the **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="7a11f-214">然後將上述程式碼範例中的 **SqlCommand** 物件宣告變更如下。</span><span class="sxs-lookup"><span data-stu-id="7a11f-214">Then change the **SqlCommand** object declaration in the previous code example to the following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="7a11f-215">在大部分情況下，資料表值參數的效能同於或高於其他批次處理技術。</span><span class="sxs-lookup"><span data-stu-id="7a11f-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="7a11f-216">資料表值參數通常較適合，因為比其他選項更有彈性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="7a11f-217">例如，其他技術 (例如 SQL 大量複製) 只允許插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-217">For example, other techniques, such as SQL bulk copy, only permit the insertion of new rows.</span></span> <span data-ttu-id="7a11f-218">但使用資料表值參數時，您可以在預存程序中使用邏輯，判斷哪些資料列是更新和哪些是插入。</span><span class="sxs-lookup"><span data-stu-id="7a11f-218">But with table-valued parameters, you can use logic in the stored procedure to determine which rows are updates and which are inserts.</span></span> <span data-ttu-id="7a11f-219">也可以修改資料表類型來包含「作業」資料行，指出是否應該插入、更新或刪除指定的資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-219">The table type can also be modified to contain an “Operation” column that indicates whether the specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="7a11f-220">下表顯示使用資料表值參數的臨機操作測試結果 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-220">The following table shows ad-hoc test results for the use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="7a11f-221">作業</span><span class="sxs-lookup"><span data-stu-id="7a11f-221">Operations</span></span> | <span data-ttu-id="7a11f-222">內部部署至 Azure (亳秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-222">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="7a11f-223">Azure 相同資料中心 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a11f-224">1</span><span class="sxs-lookup"><span data-stu-id="7a11f-224">1</span></span> |<span data-ttu-id="7a11f-225">124</span><span class="sxs-lookup"><span data-stu-id="7a11f-225">124</span></span> |<span data-ttu-id="7a11f-226">32</span><span class="sxs-lookup"><span data-stu-id="7a11f-226">32</span></span> |
| <span data-ttu-id="7a11f-227">10</span><span class="sxs-lookup"><span data-stu-id="7a11f-227">10</span></span> |<span data-ttu-id="7a11f-228">131</span><span class="sxs-lookup"><span data-stu-id="7a11f-228">131</span></span> |<span data-ttu-id="7a11f-229">25</span><span class="sxs-lookup"><span data-stu-id="7a11f-229">25</span></span> |
| <span data-ttu-id="7a11f-230">100</span><span class="sxs-lookup"><span data-stu-id="7a11f-230">100</span></span> |<span data-ttu-id="7a11f-231">338</span><span class="sxs-lookup"><span data-stu-id="7a11f-231">338</span></span> |<span data-ttu-id="7a11f-232">51</span><span class="sxs-lookup"><span data-stu-id="7a11f-232">51</span></span> |
| <span data-ttu-id="7a11f-233">1000</span><span class="sxs-lookup"><span data-stu-id="7a11f-233">1000</span></span> |<span data-ttu-id="7a11f-234">2615</span><span class="sxs-lookup"><span data-stu-id="7a11f-234">2615</span></span> |<span data-ttu-id="7a11f-235">382</span><span class="sxs-lookup"><span data-stu-id="7a11f-235">382</span></span> |
| <span data-ttu-id="7a11f-236">10000</span><span class="sxs-lookup"><span data-stu-id="7a11f-236">10000</span></span> |<span data-ttu-id="7a11f-237">23830</span><span class="sxs-lookup"><span data-stu-id="7a11f-237">23830</span></span> |<span data-ttu-id="7a11f-238">3586</span><span class="sxs-lookup"><span data-stu-id="7a11f-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="7a11f-239">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="7a11f-239">Results are not benchmarks.</span></span> <span data-ttu-id="7a11f-240">請參閱 [有關本主題中計時結果的注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-240">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="7a11f-241">批次處理所提升的效能立即而明顯。</span><span class="sxs-lookup"><span data-stu-id="7a11f-241">The performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="7a11f-242">在先前的循序測試中，1000 個作業在資料中心外花費 129 秒，而從資料中心內花費 21 秒。</span><span class="sxs-lookup"><span data-stu-id="7a11f-242">In the previous sequential test, 1000 operations took 129 seconds outside the datacenter and 21 seconds from within the datacenter.</span></span> <span data-ttu-id="7a11f-243">但使用資料表值參數時，1000 個作業在資料中心外只花費 2.6 秒，而在資料中心內只花費 0.4 秒。</span><span class="sxs-lookup"><span data-stu-id="7a11f-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside the datacenter and 0.4 seconds within the datacenter.</span></span>

<span data-ttu-id="7a11f-244">如需資料表值參數的詳細資訊，請參閱 [資料表值參數](https://msdn.microsoft.com/library/bb510489.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="7a11f-245">SQL 大量複製</span><span class="sxs-lookup"><span data-stu-id="7a11f-245">SQL bulk copy</span></span>
<span data-ttu-id="7a11f-246">SQL 大量複製是另一種將大量資料插入至目標資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="7a11f-246">SQL bulk copy is another way to insert large amounts of data into a target database.</span></span> <span data-ttu-id="7a11f-247">.NET 應用程式可以使用 **SqlBulkCopy** 類別執行大量插入作業。</span><span class="sxs-lookup"><span data-stu-id="7a11f-247">.NET applications can use the **SqlBulkCopy** class to perform bulk insert operations.</span></span> <span data-ttu-id="7a11f-248">**SqlBulkCopy** 在功能上類似於命令列工具 **Bcp.exe**，或 Transact-SQL 陳述式 **BULK INSERT**。</span><span class="sxs-lookup"><span data-stu-id="7a11f-248">**SqlBulkCopy** is similar in function to the command-line tool, **Bcp.exe**, or the Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="7a11f-249">下列程式碼範例顯示如何將來源 **DataTable**資料表中的資料列，大量複製到 SQL Server 中的目的地資料表 MyTable。</span><span class="sxs-lookup"><span data-stu-id="7a11f-249">The following code example shows how to bulk copy the rows in the source **DataTable**, table, to the destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="7a11f-250">在某些情況下，大量複製比資料表值參數更適合。</span><span class="sxs-lookup"><span data-stu-id="7a11f-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="7a11f-251">請參閱 [資料表值參數](https://msdn.microsoft.com/library/bb510489.aspx)主題中的資料表值參數與 BULK INSERT 作業的比較表。</span><span class="sxs-lookup"><span data-stu-id="7a11f-251">See the comparison table of Table-Valued parameters versus BULK INSERT operations in the topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="7a11f-252">下列臨機操作測試結果顯示 **SqlBulkCopy** 的批次處理效能 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-252">The following ad-hoc test results show the performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="7a11f-253">作業</span><span class="sxs-lookup"><span data-stu-id="7a11f-253">Operations</span></span> | <span data-ttu-id="7a11f-254">內部部署至 Azure (亳秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-254">On-Premises to Azure (ms)</span></span> | <span data-ttu-id="7a11f-255">Azure 相同資料中心 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a11f-256">1</span><span class="sxs-lookup"><span data-stu-id="7a11f-256">1</span></span> |<span data-ttu-id="7a11f-257">433</span><span class="sxs-lookup"><span data-stu-id="7a11f-257">433</span></span> |<span data-ttu-id="7a11f-258">57</span><span class="sxs-lookup"><span data-stu-id="7a11f-258">57</span></span> |
| <span data-ttu-id="7a11f-259">10</span><span class="sxs-lookup"><span data-stu-id="7a11f-259">10</span></span> |<span data-ttu-id="7a11f-260">441</span><span class="sxs-lookup"><span data-stu-id="7a11f-260">441</span></span> |<span data-ttu-id="7a11f-261">32</span><span class="sxs-lookup"><span data-stu-id="7a11f-261">32</span></span> |
| <span data-ttu-id="7a11f-262">100</span><span class="sxs-lookup"><span data-stu-id="7a11f-262">100</span></span> |<span data-ttu-id="7a11f-263">636</span><span class="sxs-lookup"><span data-stu-id="7a11f-263">636</span></span> |<span data-ttu-id="7a11f-264">53</span><span class="sxs-lookup"><span data-stu-id="7a11f-264">53</span></span> |
| <span data-ttu-id="7a11f-265">1000</span><span class="sxs-lookup"><span data-stu-id="7a11f-265">1000</span></span> |<span data-ttu-id="7a11f-266">2535</span><span class="sxs-lookup"><span data-stu-id="7a11f-266">2535</span></span> |<span data-ttu-id="7a11f-267">341</span><span class="sxs-lookup"><span data-stu-id="7a11f-267">341</span></span> |
| <span data-ttu-id="7a11f-268">10000</span><span class="sxs-lookup"><span data-stu-id="7a11f-268">10000</span></span> |<span data-ttu-id="7a11f-269">21605</span><span class="sxs-lookup"><span data-stu-id="7a11f-269">21605</span></span> |<span data-ttu-id="7a11f-270">2737</span><span class="sxs-lookup"><span data-stu-id="7a11f-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="7a11f-271">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="7a11f-271">Results are not benchmarks.</span></span> <span data-ttu-id="7a11f-272">請參閱 [有關本主題中計時結果的注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-272">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="7a11f-273">批次較小時，使用資料表值參數的效能勝過 **SqlBulkCopy** 類別。</span><span class="sxs-lookup"><span data-stu-id="7a11f-273">In smaller batch sizes, the use table-valued parameters outperformed the **SqlBulkCopy** class.</span></span> <span data-ttu-id="7a11f-274">不過，在測試 1,000 和 10,000 個資料列時，**SqlBulkCopy** 的執行速度比資料表值參數快 12-31%。</span><span class="sxs-lookup"><span data-stu-id="7a11f-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for the tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="7a11f-275">就像資料表值參數一樣， **SqlBulkCopy** 是批次插入的理想選擇，尤其與非批次作業的效能相比較。</span><span class="sxs-lookup"><span data-stu-id="7a11f-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared to the performance of non-batched operations.</span></span>

<span data-ttu-id="7a11f-276">如需 ADO.NET 中的大量複製的詳細資訊，請參閱 [SQL Server 中的大量複製作業](https://msdn.microsoft.com/library/7ek5da1a.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="7a11f-277">多資料列參數化 INSERT 陳述式</span><span class="sxs-lookup"><span data-stu-id="7a11f-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="7a11f-278">對於小型批次，另一種作法是建構大型參數化 INSERT 陳述式來插入多個資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-278">One alternative for small batches is to construct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="7a11f-279">下列程式碼範例示範這項技巧。</span><span class="sxs-lookup"><span data-stu-id="7a11f-279">The following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="7a11f-280">此範例主要是示範基本概念。</span><span class="sxs-lookup"><span data-stu-id="7a11f-280">This example is meant to show the basic concept.</span></span> <span data-ttu-id="7a11f-281">在更實際的案例中會循環查看需要的實體，以同時建構查詢字串和命令參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-281">A more realistic scenario would loop through the required entities to construct the query string and the command parameters simultaneously.</span></span> <span data-ttu-id="7a11f-282">總計以 2100 個查詢參數為限，此方法可處理的資料列總數受限於此。</span><span class="sxs-lookup"><span data-stu-id="7a11f-282">You are limited to a total of 2100 query parameters, so this limits the total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="7a11f-283">下列臨機操作測試結果顯示這種插入陳述式的效能 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-283">The following ad-hoc test results show the performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="7a11f-284">作業</span><span class="sxs-lookup"><span data-stu-id="7a11f-284">Operations</span></span> | <span data-ttu-id="7a11f-285">資料表值參數 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="7a11f-286">單一陳述式 INSERT (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a11f-287">1</span><span class="sxs-lookup"><span data-stu-id="7a11f-287">1</span></span> |<span data-ttu-id="7a11f-288">32</span><span class="sxs-lookup"><span data-stu-id="7a11f-288">32</span></span> |<span data-ttu-id="7a11f-289">20</span><span class="sxs-lookup"><span data-stu-id="7a11f-289">20</span></span> |
| <span data-ttu-id="7a11f-290">10</span><span class="sxs-lookup"><span data-stu-id="7a11f-290">10</span></span> |<span data-ttu-id="7a11f-291">30</span><span class="sxs-lookup"><span data-stu-id="7a11f-291">30</span></span> |<span data-ttu-id="7a11f-292">25</span><span class="sxs-lookup"><span data-stu-id="7a11f-292">25</span></span> |
| <span data-ttu-id="7a11f-293">100</span><span class="sxs-lookup"><span data-stu-id="7a11f-293">100</span></span> |<span data-ttu-id="7a11f-294">33</span><span class="sxs-lookup"><span data-stu-id="7a11f-294">33</span></span> |<span data-ttu-id="7a11f-295">51</span><span class="sxs-lookup"><span data-stu-id="7a11f-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="7a11f-296">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="7a11f-296">Results are not benchmarks.</span></span> <span data-ttu-id="7a11f-297">請參閱 [有關本主題中計時結果的注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-297">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="7a11f-298">如果批次少於 100 的資料列，這種方法會稍微快一些。</span><span class="sxs-lookup"><span data-stu-id="7a11f-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="7a11f-299">雖然改善幅度很小，但在您的特殊應用案例中，這種技術可能是另一種適合的選項。</span><span class="sxs-lookup"><span data-stu-id="7a11f-299">Although the improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="7a11f-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="7a11f-300">DataAdapter</span></span>
<span data-ttu-id="7a11f-301">**DataAdapter** 類別可讓您修改 **DataSet** 物件，然後以 INSERT、UPDATE 和 DELETE 作業的形式提交變更。</span><span class="sxs-lookup"><span data-stu-id="7a11f-301">The **DataAdapter** class allows you to modify a **DataSet** object and then submit the changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="7a11f-302">如果以此方式使用 **DataAdapter** ，必須注意每個不同的作業會執行個別的呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-302">If you are using the **DataAdapter** in this manner, it is important to note that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="7a11f-303">若要改善效能，請使用 **UpdateBatchSize** 屬性指定應該同時批次處理的作業數目。</span><span class="sxs-lookup"><span data-stu-id="7a11f-303">To improve performance, use the **UpdateBatchSize** property to the number of operations that should be batched at a time.</span></span> <span data-ttu-id="7a11f-304">如需詳細資訊，請參閱 [使用 Dataadapter 執行批次作業](https://msdn.microsoft.com/library/aadf8fk2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="7a11f-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="7a11f-305">Entity framework</span></span>
<span data-ttu-id="7a11f-306">Entity Framework 目前不支援批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="7a11f-307">社群中不同的開發人員已嘗試示範因應措施，例如覆寫 **SaveChanges** 方法。</span><span class="sxs-lookup"><span data-stu-id="7a11f-307">Different developers in the community have attempted to demonstrate workarounds, such as override the **SaveChanges** method.</span></span> <span data-ttu-id="7a11f-308">但解決方案通常太複雜，而且都針對應用程式和資料模型來自訂。</span><span class="sxs-lookup"><span data-stu-id="7a11f-308">But the solutions are typically complex and customized to the application and data model.</span></span> <span data-ttu-id="7a11f-309">Entity Framework codeplex 專案目前有這項功能要求的討論頁。</span><span class="sxs-lookup"><span data-stu-id="7a11f-309">The Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="7a11f-310">若要查看這項討論，請參閱[設計會議記錄 - 2012 年 8 月 2 日 (英文)](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-310">To view this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="7a11f-311">XML</span><span class="sxs-lookup"><span data-stu-id="7a11f-311">XML</span></span>
<span data-ttu-id="7a11f-312">為了完整說明，我們覺得有必要討論將 XML 當做批次處理策略。</span><span class="sxs-lookup"><span data-stu-id="7a11f-312">For completeness, we feel that it is important to talk about XML as a batching strategy.</span></span> <span data-ttu-id="7a11f-313">但是，使用 XML 沒有比其他方法更好，而且還有幾個缺點。</span><span class="sxs-lookup"><span data-stu-id="7a11f-313">However, the use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="7a11f-314">此方法類似於資料表值參數，但傳給預存程序的是 XML 檔案或字串，而不是使用者定義的資料表。</span><span class="sxs-lookup"><span data-stu-id="7a11f-314">The approach is similar to table-valued parameters, but an XML file or string is passed to a stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="7a11f-315">預存程序會剖析預存程序中的命令。</span><span class="sxs-lookup"><span data-stu-id="7a11f-315">The stored procedure parses the commands in the stored procedure.</span></span>

<span data-ttu-id="7a11f-316">這種方法有幾個缺點：</span><span class="sxs-lookup"><span data-stu-id="7a11f-316">There are several disadvantages to this approach:</span></span>

* <span data-ttu-id="7a11f-317">處理 XML 很麻煩又容易出錯。</span><span class="sxs-lookup"><span data-stu-id="7a11f-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="7a11f-318">在資料庫上剖析 XML 會耗用大量 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="7a11f-318">Parsing the XML on the database can be CPU-intensive.</span></span>
* <span data-ttu-id="7a11f-319">在大部分情況下，這種方法比資料表值參數更慢。</span><span class="sxs-lookup"><span data-stu-id="7a11f-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="7a11f-320">基於這些理由，不建議使用 XML 進行批次查詢。</span><span class="sxs-lookup"><span data-stu-id="7a11f-320">For these reasons, the use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="7a11f-321">批次處理考量</span><span class="sxs-lookup"><span data-stu-id="7a11f-321">Batching considerations</span></span>
<span data-ttu-id="7a11f-322">下列各節提供在 SQL Database 應用程式中使用批次處理的其他指引。</span><span class="sxs-lookup"><span data-stu-id="7a11f-322">The following sections provide more guidance for the use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="7a11f-323">權衡取捨</span><span class="sxs-lookup"><span data-stu-id="7a11f-323">Tradeoffs</span></span>
<span data-ttu-id="7a11f-324">根據您的架構而定，批次處理可能需要在效能和恢復功能之間有所取捨。</span><span class="sxs-lookup"><span data-stu-id="7a11f-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="7a11f-325">例如，假設您的角色非預期地停止運作。</span><span class="sxs-lookup"><span data-stu-id="7a11f-325">For example, consider the scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="7a11f-326">如果您失去一個資料列，影響程度會小於遺失一大批尚未提交的資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-326">If you lose one row of data, the impact is smaller than the impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="7a11f-327">將資料列傳送至資料庫之前，如果您將資料列緩衝一段指定的時間，則風險會很高。</span><span class="sxs-lookup"><span data-stu-id="7a11f-327">There is a greater risk when you buffer rows before sending them to the database in a specified time window.</span></span>

<span data-ttu-id="7a11f-328">由於有這種權衡取捨，請評估您要批次處理的作業類型。</span><span class="sxs-lookup"><span data-stu-id="7a11f-328">Because of this tradeoff, evaluate the type of operations that you batch.</span></span> <span data-ttu-id="7a11f-329">對於較不重要的資料，應該更積極地批次處理 (較大的批次和較長的時間範圍)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="7a11f-330">批次大小</span><span class="sxs-lookup"><span data-stu-id="7a11f-330">Batch size</span></span>
<span data-ttu-id="7a11f-331">在我們的測試中，將大型批次分成小塊通常沒有好處。</span><span class="sxs-lookup"><span data-stu-id="7a11f-331">In our tests, there was typically no advantage to breaking large batches into smaller chunks.</span></span> <span data-ttu-id="7a11f-332">事實上，這樣分割通常會導致效能比提交單一大型批次更慢。</span><span class="sxs-lookup"><span data-stu-id="7a11f-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="7a11f-333">例如，假設您想要插入 1000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-333">For example, consider a scenario where you want to insert 1000 rows.</span></span> <span data-ttu-id="7a11f-334">下表顯示分割成較小的批次時，使用資料表值參數插入 1000 個資料列所需的時間。</span><span class="sxs-lookup"><span data-stu-id="7a11f-334">The following table shows how long it takes to use table-valued parameters to insert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="7a11f-335">批次大小</span><span class="sxs-lookup"><span data-stu-id="7a11f-335">Batch size</span></span> | <span data-ttu-id="7a11f-336">反覆運算次數</span><span class="sxs-lookup"><span data-stu-id="7a11f-336">Iterations</span></span> | <span data-ttu-id="7a11f-337">資料表值參數 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7a11f-338">1000</span><span class="sxs-lookup"><span data-stu-id="7a11f-338">1000</span></span> |<span data-ttu-id="7a11f-339">1</span><span class="sxs-lookup"><span data-stu-id="7a11f-339">1</span></span> |<span data-ttu-id="7a11f-340">347</span><span class="sxs-lookup"><span data-stu-id="7a11f-340">347</span></span> |
| <span data-ttu-id="7a11f-341">500</span><span class="sxs-lookup"><span data-stu-id="7a11f-341">500</span></span> |<span data-ttu-id="7a11f-342">2</span><span class="sxs-lookup"><span data-stu-id="7a11f-342">2</span></span> |<span data-ttu-id="7a11f-343">355</span><span class="sxs-lookup"><span data-stu-id="7a11f-343">355</span></span> |
| <span data-ttu-id="7a11f-344">100</span><span class="sxs-lookup"><span data-stu-id="7a11f-344">100</span></span> |<span data-ttu-id="7a11f-345">10</span><span class="sxs-lookup"><span data-stu-id="7a11f-345">10</span></span> |<span data-ttu-id="7a11f-346">465</span><span class="sxs-lookup"><span data-stu-id="7a11f-346">465</span></span> |
| <span data-ttu-id="7a11f-347">50</span><span class="sxs-lookup"><span data-stu-id="7a11f-347">50</span></span> |<span data-ttu-id="7a11f-348">20</span><span class="sxs-lookup"><span data-stu-id="7a11f-348">20</span></span> |<span data-ttu-id="7a11f-349">630</span><span class="sxs-lookup"><span data-stu-id="7a11f-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="7a11f-350">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="7a11f-350">Results are not benchmarks.</span></span> <span data-ttu-id="7a11f-351">請參閱 [有關本主題中計時結果的注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-351">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="7a11f-352">您可以看出，將 1000 個資料列一次全部提交，才能獲得最佳效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-352">You can see that the best performance for 1000 rows is to submit them all at once.</span></span> <span data-ttu-id="7a11f-353">在其他測試中 (這裡未顯示)，將 10000 個資料列的批次分成兩個各有 5000 個資料列的批次會稍微提高效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-353">In other tests (not shown here) there was a small performance gain to break a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="7a11f-354">但是這些測試的資料表結構描述相當簡單，您應該針對您的特定資料和批次大小進行測試，以確認這些研究結果。</span><span class="sxs-lookup"><span data-stu-id="7a11f-354">But the table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes to verify these findings.</span></span>

<span data-ttu-id="7a11f-355">另一個要考量的因素是如果整個批次變得太大，SQL Database 可能會節流並拒絕認可批次。</span><span class="sxs-lookup"><span data-stu-id="7a11f-355">Another factor to consider is that if the total batch becomes too large, SQL Database might throttle and refuse to commit the batch.</span></span> <span data-ttu-id="7a11f-356">為了獲得最佳結果，請測試您的特定案例，以判斷是否有較理想的批次大小。</span><span class="sxs-lookup"><span data-stu-id="7a11f-356">For the best results, test your specific scenario to determine if there is an ideal batch size.</span></span> <span data-ttu-id="7a11f-357">允許在執行階段設定批次大小，以根據效能或錯誤來快速調整。</span><span class="sxs-lookup"><span data-stu-id="7a11f-357">Make the batch size configurable at runtime to enable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="7a11f-358">最後，在批次大小與批次處理相關的風險之間找出平衡點。</span><span class="sxs-lookup"><span data-stu-id="7a11f-358">Finally, balance the size of the batch with the risks associated with batching.</span></span> <span data-ttu-id="7a11f-359">如果發生暫時性錯誤或角色失敗，請考量重試作業或遺失批次中的資料的後果。</span><span class="sxs-lookup"><span data-stu-id="7a11f-359">If there are transient errors or the role fails, consider the consequences of retrying the operation or of losing the data in the batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="7a11f-360">平行處理</span><span class="sxs-lookup"><span data-stu-id="7a11f-360">Parallel processing</span></span>
<span data-ttu-id="7a11f-361">如果您已設法縮小批次，但使用多個執行緒來執行工作，情況又是如何？</span><span class="sxs-lookup"><span data-stu-id="7a11f-361">What if you took the approach of reducing the batch size but used multiple threads to execute the work?</span></span> <span data-ttu-id="7a11f-362">同樣地，我們的測試指出數個較小的多執行緒批次通常表現得比單一大型批次更差。</span><span class="sxs-lookup"><span data-stu-id="7a11f-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="7a11f-363">下列測試嘗試透過一或多個平行批次來插入 1000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-363">The following test attempts to insert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="7a11f-364">此測試指出同時有多個批次實際上會降低效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="7a11f-365">批次大小 [反覆運算次數]</span><span class="sxs-lookup"><span data-stu-id="7a11f-365">Batch size [Iterations]</span></span> | <span data-ttu-id="7a11f-366">兩個執行緒 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-366">Two threads (ms)</span></span> | <span data-ttu-id="7a11f-367">四個執行緒 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-367">Four threads (ms)</span></span> | <span data-ttu-id="7a11f-368">六個執行緒 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="7a11f-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a11f-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="7a11f-369">1000 [1]</span></span> |<span data-ttu-id="7a11f-370">277</span><span class="sxs-lookup"><span data-stu-id="7a11f-370">277</span></span> |<span data-ttu-id="7a11f-371">315</span><span class="sxs-lookup"><span data-stu-id="7a11f-371">315</span></span> |<span data-ttu-id="7a11f-372">266</span><span class="sxs-lookup"><span data-stu-id="7a11f-372">266</span></span> |
| <span data-ttu-id="7a11f-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="7a11f-373">500 [2]</span></span> |<span data-ttu-id="7a11f-374">548</span><span class="sxs-lookup"><span data-stu-id="7a11f-374">548</span></span> |<span data-ttu-id="7a11f-375">278</span><span class="sxs-lookup"><span data-stu-id="7a11f-375">278</span></span> |<span data-ttu-id="7a11f-376">256</span><span class="sxs-lookup"><span data-stu-id="7a11f-376">256</span></span> |
| <span data-ttu-id="7a11f-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="7a11f-377">250 [4]</span></span> |<span data-ttu-id="7a11f-378">405</span><span class="sxs-lookup"><span data-stu-id="7a11f-378">405</span></span> |<span data-ttu-id="7a11f-379">329</span><span class="sxs-lookup"><span data-stu-id="7a11f-379">329</span></span> |<span data-ttu-id="7a11f-380">265</span><span class="sxs-lookup"><span data-stu-id="7a11f-380">265</span></span> |
| <span data-ttu-id="7a11f-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="7a11f-381">100 [10]</span></span> |<span data-ttu-id="7a11f-382">488</span><span class="sxs-lookup"><span data-stu-id="7a11f-382">488</span></span> |<span data-ttu-id="7a11f-383">439</span><span class="sxs-lookup"><span data-stu-id="7a11f-383">439</span></span> |<span data-ttu-id="7a11f-384">391</span><span class="sxs-lookup"><span data-stu-id="7a11f-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="7a11f-385">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="7a11f-385">Results are not benchmarks.</span></span> <span data-ttu-id="7a11f-386">請參閱 [有關本主題中計時結果的注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-386">See the [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="7a11f-387">由於平行處理而造成效能下降可能有幾個原因：</span><span class="sxs-lookup"><span data-stu-id="7a11f-387">There are several potential reasons for the degradation in performance due to parallelism:</span></span>

* <span data-ttu-id="7a11f-388">同時有多個網路呼叫，而不只一個。</span><span class="sxs-lookup"><span data-stu-id="7a11f-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="7a11f-389">對單一資料表執行多個作業會導致爭用和鎖定。</span><span class="sxs-lookup"><span data-stu-id="7a11f-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="7a11f-390">多執行緒處理會引起額外負荷。</span><span class="sxs-lookup"><span data-stu-id="7a11f-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="7a11f-391">開啟多個連接的成本超過平行處理的效益。</span><span class="sxs-lookup"><span data-stu-id="7a11f-391">The expense of opening multiple connections outweighs the benefit of parallel processing.</span></span>

<span data-ttu-id="7a11f-392">如果以不同資料表或資料庫為目標，這種策略可能會提高一些效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-392">If you target different tables or databases, it is possible to see some performance gain with this strategy.</span></span> <span data-ttu-id="7a11f-393">資料庫分區化或同盟就是適合這種方法的案例。</span><span class="sxs-lookup"><span data-stu-id="7a11f-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="7a11f-394">分區化會使用多個資料庫，並將不同資料路由傳送至每個資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-394">Sharding uses multiple databases and routes different data to each database.</span></span> <span data-ttu-id="7a11f-395">如果每個小批次各送往不同的資料庫，則以平行方式執行作業會更有效率。</span><span class="sxs-lookup"><span data-stu-id="7a11f-395">If each small batch is going to a different database, then performing the operations in parallel can be more efficient.</span></span> <span data-ttu-id="7a11f-396">但是，效能提升不顯著，難以據此決定在您的解決方案中使用資料庫分區化。</span><span class="sxs-lookup"><span data-stu-id="7a11f-396">However, the performance gain is not significant enough to use as the basis for a decision to use database sharding in your solution.</span></span>

<span data-ttu-id="7a11f-397">在某些設計中，平行執行較小的批次可以在負載不足的系統中改善要求輸送量。</span><span class="sxs-lookup"><span data-stu-id="7a11f-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="7a11f-398">在此情況下，即使處理單一大型批次更快速，但以平行方式處理多個批次可能更有效率。</span><span class="sxs-lookup"><span data-stu-id="7a11f-398">In this case, even though it is quicker to process a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="7a11f-399">如果您使用平行執行，請考慮控制背景工作角色執行緒的數目上限。</span><span class="sxs-lookup"><span data-stu-id="7a11f-399">If you do use parallel execution, consider controlling the maximum number of worker threads.</span></span> <span data-ttu-id="7a11f-400">數量較少可以減少爭用，並加快執行時間。</span><span class="sxs-lookup"><span data-stu-id="7a11f-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="7a11f-401">另外，也要考慮這在連接和交易中對目標資料庫所造成的額外負載。</span><span class="sxs-lookup"><span data-stu-id="7a11f-401">Also, consider the additional load that this places on the target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="7a11f-402">相關的效能因素</span><span class="sxs-lookup"><span data-stu-id="7a11f-402">Related performance factors</span></span>
<span data-ttu-id="7a11f-403">資料庫效能的一般指引也會影響批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="7a11f-404">例如，如果資料表具有大型的主索引鍵或許多非叢集索引，插入效能會降低。</span><span class="sxs-lookup"><span data-stu-id="7a11f-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="7a11f-405">如果資料表值參數使用預存程序，您可以在程序的開頭使用命令 **SET NOCOUNT ON** 。</span><span class="sxs-lookup"><span data-stu-id="7a11f-405">If table-valued parameters use a stored procedure, you can use the command **SET NOCOUNT ON** at the beginning of the procedure.</span></span> <span data-ttu-id="7a11f-406">這個陳述式會防止傳回程序中受影響的資料列計數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-406">This statement suppresses the return of the count of the affected rows in the procedure.</span></span> <span data-ttu-id="7a11f-407">不過，在我們的測試中，使用 **SET NOCOUNT ON** 不是沒有效果，就是降低效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-407">However, in our tests, the use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="7a11f-408">測試預存程序很簡單，只有來自資料表值參數的單一 **INSERT** 命令。</span><span class="sxs-lookup"><span data-stu-id="7a11f-408">The test stored procedure was simple with a single **INSERT** command from the table-valued parameter.</span></span> <span data-ttu-id="7a11f-409">此陳述式可能有益於更複雜的預存程序。</span><span class="sxs-lookup"><span data-stu-id="7a11f-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="7a11f-410">但別以為將 **SET NOCOUNT ON** 新增至預存程序就會自動改善效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-410">But don’t assume that adding **SET NOCOUNT ON** to your stored procedure automatically improves performance.</span></span> <span data-ttu-id="7a11f-411">若要了解效果，請分別使用和不使用 **SET NOCOUNT ON** 陳述式來測試預存程序。</span><span class="sxs-lookup"><span data-stu-id="7a11f-411">To understand the effect, test your stored procedure with and without the **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="7a11f-412">批次處理案例</span><span class="sxs-lookup"><span data-stu-id="7a11f-412">Batching scenarios</span></span>
<span data-ttu-id="7a11f-413">下列各節說明如何在三個應用程式案例中使用資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-413">The following sections describe how to use table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="7a11f-414">第一個案例示範緩衝和批次處理如何一起運作。</span><span class="sxs-lookup"><span data-stu-id="7a11f-414">The first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="7a11f-415">第二個案例在單一預存程序呼叫中執行主要/詳細架構作業以提高效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-415">The second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="7a11f-416">最後一個案例示範如何在 "UPSERT" 作業中使用資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-416">The final scenario shows how to use table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="7a11f-417">緩衝處理</span><span class="sxs-lookup"><span data-stu-id="7a11f-417">Buffering</span></span>
<span data-ttu-id="7a11f-418">雖然有些案例很明顯適合使用批次處理，但也有許多案例可以藉由延遲處理來利用批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="7a11f-419">不過，延遲處理也會帶來更大的風險，發生非預期的失敗時會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="7a11f-419">However, delayed processing also carries a greater risk that the data is lost in the event of an unexpected failure.</span></span> <span data-ttu-id="7a11f-420">請務必了解這項風險並考慮後果。</span><span class="sxs-lookup"><span data-stu-id="7a11f-420">It is important to understand this risk and consider the consequences.</span></span>

<span data-ttu-id="7a11f-421">例如，假設有一個 Web 應用程式會追蹤每一位使用者的瀏覽歷程記錄。</span><span class="sxs-lookup"><span data-stu-id="7a11f-421">For example, consider a web application that tracks the navigation history of each user.</span></span> <span data-ttu-id="7a11f-422">在每個頁面要求上，應用程式會執行資料庫呼叫來記錄使用者的頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="7a11f-422">On each page request, the application could make a database call to record the user’s page view.</span></span> <span data-ttu-id="7a11f-423">但只要緩衝使用者的瀏覽活動，再分批將此資料傳送至資料庫，就能達到更高的效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-423">But higher performance and scalability can be achieved by buffering the users’ navigation activities and then sending this data to the database in batches.</span></span> <span data-ttu-id="7a11f-424">您可以指定經歷時間和 (或) 緩衝區大小來觸發資料庫更新。</span><span class="sxs-lookup"><span data-stu-id="7a11f-424">You can trigger the database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="7a11f-425">例如，規則可以指定應該在 20 秒之後或緩衝區達到 1000 個項目時處理批次。</span><span class="sxs-lookup"><span data-stu-id="7a11f-425">For example, a rule could specify that the batch should be processed after 20 seconds or when the buffer reaches 1000 items.</span></span>

<span data-ttu-id="7a11f-426">下列程式碼範例使用 [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) 處理監視類別所引發的緩衝事件。</span><span class="sxs-lookup"><span data-stu-id="7a11f-426">The following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) to process buffered events raised by a monitoring class.</span></span> <span data-ttu-id="7a11f-427">當緩衝區填滿或達到逾時，就透過資料表值參數將使用者資料的批次傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-427">When the buffer fills or a timeout is reached, the batch of user data is sent to the database with a table-valued parameter.</span></span>

<span data-ttu-id="7a11f-428">下列 NavHistoryData 類別塑造使用者瀏覽詳細資料的模型。</span><span class="sxs-lookup"><span data-stu-id="7a11f-428">The following NavHistoryData class models the user navigation details.</span></span> <span data-ttu-id="7a11f-429">它包含使用者識別碼、存取的 URL 和存取時間等基本資訊。</span><span class="sxs-lookup"><span data-stu-id="7a11f-429">It contains basic information such as the user identifier, the URL accessed, and the access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="7a11f-430">NavHistoryDataMonitor 類別負責將使用者瀏覽資料緩衝處理到資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-430">The NavHistoryDataMonitor class is responsible for buffering the user navigation data to the database.</span></span> <span data-ttu-id="7a11f-431">它包含 RecordUserNavigationEntry 方法，以引發 **OnAdded** 事件做為回應。</span><span class="sxs-lookup"><span data-stu-id="7a11f-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="7a11f-432">下列程式碼顯示建構函式邏輯，其中使用 Rx 根據事件建立可觀察的集合。</span><span class="sxs-lookup"><span data-stu-id="7a11f-432">The following code shows the constructor logic that uses Rx to create an observable collection based on the event.</span></span> <span data-ttu-id="7a11f-433">它接著使用 Buffer 方法訂閱這個可觀察的集合。</span><span class="sxs-lookup"><span data-stu-id="7a11f-433">It then subscribes to this observable collection with the Buffer method.</span></span> <span data-ttu-id="7a11f-434">此多載函式指定每隔 20 秒或 1000 個項目就應該傳送緩衝區。</span><span class="sxs-lookup"><span data-stu-id="7a11f-434">The overload specifies that the buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="7a11f-435">此處理常式會將所有緩衝項目轉換成資料表值類型，然後將此類型傳遞給處理批次的預存程序。</span><span class="sxs-lookup"><span data-stu-id="7a11f-435">The handler converts all of the buffered items into a table-valued type and then passes this type to a stored procedure that processes the batch.</span></span> <span data-ttu-id="7a11f-436">下列程式碼顯示 NavHistoryDataEventArgs 和 NavHistoryDataMonitor 類別的完整定義。</span><span class="sxs-lookup"><span data-stu-id="7a11f-436">The following code shows the complete definition for both the NavHistoryDataEventArgs and the NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="7a11f-437">若要使用這個緩衝類別，應用程式需要建立靜態 NavHistoryDataMonitor 物件。</span><span class="sxs-lookup"><span data-stu-id="7a11f-437">To use this buffering class, the application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="7a11f-438">每次使用者存取頁面時，應用程式就呼叫 NavHistoryDataMonitor.RecordUserNavigationEntry 方法。</span><span class="sxs-lookup"><span data-stu-id="7a11f-438">Each time a user accesses a page, the application calls the NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="7a11f-439">緩衝邏輯接著負責將這些項目分批傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-439">The buffering logic proceeds to take care of sending these entries to the database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="7a11f-440">主要/詳細架構</span><span class="sxs-lookup"><span data-stu-id="7a11f-440">Master detail</span></span>
<span data-ttu-id="7a11f-441">資料表值參數適用於簡單的 INSERT 案例。</span><span class="sxs-lookup"><span data-stu-id="7a11f-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="7a11f-442">但是，如果插入作業涉及多個資料表，則批次處理會較具挑戰性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-442">However, it can be more challenging to batch inserts that involve more than one table.</span></span> <span data-ttu-id="7a11f-443">「主要/詳細架構」案例是一個很好的例子。</span><span class="sxs-lookup"><span data-stu-id="7a11f-443">The “master/detail” scenario is a good example.</span></span> <span data-ttu-id="7a11f-444">主要資料表識別主要實體。</span><span class="sxs-lookup"><span data-stu-id="7a11f-444">The master table identifies the primary entity.</span></span> <span data-ttu-id="7a11f-445">一或多個詳細資料表儲存實體的其他相關資料。</span><span class="sxs-lookup"><span data-stu-id="7a11f-445">One or more detail tables store more data about the entity.</span></span> <span data-ttu-id="7a11f-446">在此案例中，外部索引鍵關聯性會強制執行詳細資料與唯一主要實體的關聯性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-446">In this scenario, foreign key relationships enforce the relationship of details to a unique master entity.</span></span> <span data-ttu-id="7a11f-447">假設有一個簡化版的 PurchaseOrder 資料表及其相關聯的 OrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="7a11f-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="7a11f-448">下列 Transact-SQL 會建立具有四個資料行的 PurchaseOrder 資料表：OrderID、OrderDate、CustomerID 和 Status。</span><span class="sxs-lookup"><span data-stu-id="7a11f-448">The following Transact-SQL creates the PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="7a11f-449">每筆訂單包含一或多個產品採購。</span><span class="sxs-lookup"><span data-stu-id="7a11f-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="7a11f-450">PurchaseOrderDetail 資料表中擷取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="7a11f-450">This information is captured in the PurchaseOrderDetail table.</span></span> <span data-ttu-id="7a11f-451">下列 Transact-SQL 會建立具有五個資料行的 PurchaseOrderDetail 資料表：OrderID、OrderDetailID、ProductID、UnitPrice 和 OrderQty。</span><span class="sxs-lookup"><span data-stu-id="7a11f-451">The following Transact-SQL creates the PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="7a11f-452">PurchaseOrderDetail 資料表中的 OrderID 資料行必須參考 PurchaseOrder 資料表中的訂單。</span><span class="sxs-lookup"><span data-stu-id="7a11f-452">The OrderID column in the PurchaseOrderDetail table must reference an order from the PurchaseOrder table.</span></span> <span data-ttu-id="7a11f-453">下列的外部索引鍵定義強制執行這個限制。</span><span class="sxs-lookup"><span data-stu-id="7a11f-453">The following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="7a11f-454">若要使用資料表值參數，您必須針對每個目標資料表定義一個使用者定義資料表類型。</span><span class="sxs-lookup"><span data-stu-id="7a11f-454">In order to use table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="7a11f-455">然後，定義一個可接受這幾種資料表的預存程序。</span><span class="sxs-lookup"><span data-stu-id="7a11f-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="7a11f-456">此程序可讓應用程式以單一呼叫在本機批次處理一組訂單和訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a11f-456">This procedure allows an application to locally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="7a11f-457">下列 Transact-SQL 提供這個採購單範例的完整預存程序宣告。</span><span class="sxs-lookup"><span data-stu-id="7a11f-457">The following Transact-SQL provides the complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects the order identifiers in the @orders
    -- table with the actual order identifiers in the PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders to the PurchaseOrder table, storing the actual
    -- order identifiers in the @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match the passed-in order identifiers with the actual identifiers
    -- and complete the @IdentityLink table for use with inserting the details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert the order details into the PurchaseOrderDetail table, 
          -- using the actual order identifiers of the master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="7a11f-458">在此範例中，本機定義的 @IdentityLink 資料表會儲存新插入的資料列中的實際 OrderID 值。</span><span class="sxs-lookup"><span data-stu-id="7a11f-458">In this example, the locally defined @IdentityLink table stores the actual OrderID values from the newly inserted rows.</span></span> <span data-ttu-id="7a11f-459">這些訂單識別碼與 @orders 和 @details 資料表值參數中的暫時 OrderID 值不同。</span><span class="sxs-lookup"><span data-stu-id="7a11f-459">These order identifiers are different from the temporary OrderID values in the @orders and @details table-valued parameters.</span></span> <span data-ttu-id="7a11f-460">因此，@IdentityLink 資料表就會將 @orders 參數中的 OrderID 值，連接到 PurchaseOrder 資料表中的新資料列的實際 OrderID 值。</span><span class="sxs-lookup"><span data-stu-id="7a11f-460">For this reason, the @IdentityLink table then connects the OrderID values from the @orders parameter to the real OrderID values for the new rows in the PurchaseOrder table.</span></span> <span data-ttu-id="7a11f-461">完成這個步驟之後，@IdentityLink 資料表就能以滿足外部索引鍵條件約束的實際 OrderID，協助插入訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7a11f-461">After this step, the @IdentityLink table can facilitate inserting the order details with the actual OrderID that satisfies the foreign key constraint.</span></span>

<span data-ttu-id="7a11f-462">從程式碼或其他 Transact-SQL 呼叫中，都可以使用這個預存程序。</span><span class="sxs-lookup"><span data-stu-id="7a11f-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="7a11f-463">請參閱本文的資料表值參數一節，其中有一個程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="7a11f-463">See the table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="7a11f-464">下列 Transact-SQL 示範如何呼叫 sp_InsertOrdersBatch。</span><span class="sxs-lookup"><span data-stu-id="7a11f-464">The following Transact-SQL shows how to call the sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="7a11f-465">這個解決方案可讓每個批次使用一組從 1 開始的 OrderID 值。</span><span class="sxs-lookup"><span data-stu-id="7a11f-465">This solution allows each batch to use a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="7a11f-466">這些暫時 OrderID 值描述批次中的關聯性，但實際 OrderID 值是在插入時才決定。</span><span class="sxs-lookup"><span data-stu-id="7a11f-466">These temporary OrderID values describe the relationships in the batch, but the actual OrderID values are determined at the time of the insert operation.</span></span> <span data-ttu-id="7a11f-467">您可以重複執行上述範例中相同的陳述式，在資料庫中產生唯一的訂單。</span><span class="sxs-lookup"><span data-stu-id="7a11f-467">You can run the same statements in the previous example repeatedly and generate unique orders in the database.</span></span> <span data-ttu-id="7a11f-468">因此，使用這種批次技術時，請考慮新增更多程式碼或資料庫邏輯，以防止訂單重複。</span><span class="sxs-lookup"><span data-stu-id="7a11f-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="7a11f-469">此範例示範即使是更複雜的資料庫作業，例如主要/詳細架構作業，也都可以透過資料表值參數進行批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="7a11f-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="7a11f-470">UPSERT</span></span>
<span data-ttu-id="7a11f-471">另一個批次處理案例涉及同時更新現有的資料列和插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="7a11f-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="7a11f-472">這項作業有時稱為 "UPSERT" (更新 + 插入) 作業。</span><span class="sxs-lookup"><span data-stu-id="7a11f-472">This operation is sometimes referred to as an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="7a11f-473">MERGE 陳述式最適合這項作業，而不是分開呼叫 INSERT 和 UPDATE。</span><span class="sxs-lookup"><span data-stu-id="7a11f-473">Rather than making separate calls to INSERT and UPDATE, the MERGE statement is best suited to this task.</span></span> <span data-ttu-id="7a11f-474">MERGE 陳述式可以在單一呼叫中同時執行插入和更新作業。</span><span class="sxs-lookup"><span data-stu-id="7a11f-474">The MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="7a11f-475">資料表值參數可以搭配 MERGE 陳述式來執行更新和插入。</span><span class="sxs-lookup"><span data-stu-id="7a11f-475">Table-valued parameters can be used with the MERGE statement to perform updates and inserts.</span></span> <span data-ttu-id="7a11f-476">例如，假設有一個簡化的 Employee 資料表，包含下列資料行：EmployeeID、FirstName、LastName、SocialSecurityNumber：</span><span class="sxs-lookup"><span data-stu-id="7a11f-476">For example, consider a simplified Employee table that contains the following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="7a11f-477">在此範例中，根據 SocialSecurityNumber 是唯一性的這項事實，您可以將多個員工 MERGE。</span><span class="sxs-lookup"><span data-stu-id="7a11f-477">In this example, you can use the fact that the SocialSecurityNumber is unique to perform a MERGE of multiple employees.</span></span> <span data-ttu-id="7a11f-478">首先，建立使用者定義的資料表類型：</span><span class="sxs-lookup"><span data-stu-id="7a11f-478">First, create the user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="7a11f-479">接下來，建立預存程序或撰寫程式碼，使用 MERGE 陳述式來執行更新和插入。</span><span class="sxs-lookup"><span data-stu-id="7a11f-479">Next, create a stored procedure or write code that uses the MERGE statement to perform the update and insert.</span></span> <span data-ttu-id="7a11f-480">下列範例對 EmployeeTableType 類型的資料表值參數 @employees 使用 MERGE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="7a11f-480">The following example uses the MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="7a11f-481">此處未顯示 @employees 資料表的內容。</span><span class="sxs-lookup"><span data-stu-id="7a11f-481">The contents of the @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="7a11f-482">如需詳細資訊，請參閱 MERGE 陳述式的文件和範例。</span><span class="sxs-lookup"><span data-stu-id="7a11f-482">For more information, see the documentation and examples for the MERGE statement.</span></span> <span data-ttu-id="7a11f-483">雖然在多步驟的預存程序呼叫中搭配個別的 INSERT 和 UPDATE 作業，也能執行相同的工作，但 MERGE 陳述式會更有效率。</span><span class="sxs-lookup"><span data-stu-id="7a11f-483">Although the same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, the MERGE statement is more efficient.</span></span> <span data-ttu-id="7a11f-484">資料庫程式碼也可以建構 Transact-SQL 呼叫，直接使用 MERGE 陳述式，而不需要為 INSERT 和 UPDATE 而分別執行兩次資料庫呼叫。</span><span class="sxs-lookup"><span data-stu-id="7a11f-484">Database code can also construct Transact-SQL calls that use the MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="7a11f-485">建議摘要</span><span class="sxs-lookup"><span data-stu-id="7a11f-485">Recommendation summary</span></span>
<span data-ttu-id="7a11f-486">下列清單提供本主題中討論的批次處理建議的摘要：</span><span class="sxs-lookup"><span data-stu-id="7a11f-486">The following list provides a summary of the batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="7a11f-487">使用緩衝處理和批次處理，提高 SQL Database 應用程式的效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-487">Use buffering and batching to increase the performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="7a11f-488">了解批次處理/緩衝處理和恢復功能之間的權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="7a11f-488">Understand the tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="7a11f-489">在角色失敗期間，可能遺失一批尚未處理的商務關鍵資料，這種風險超過批次處理帶來的效能優點。</span><span class="sxs-lookup"><span data-stu-id="7a11f-489">During a role failure, the risk of losing an unprocessed batch of business-critical data might outweigh the performance benefit of batching.</span></span>
* <span data-ttu-id="7a11f-490">嘗試將所有資料庫呼叫納入單一資料中心以縮短延遲。</span><span class="sxs-lookup"><span data-stu-id="7a11f-490">Attempt to keep all calls to the database within a single datacenter to reduce latency.</span></span>
* <span data-ttu-id="7a11f-491">如果選擇單一批次處理技術，資料表值參數可以發揮最佳的效能與彈性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-491">If you choose a single batching technique, table-valued parameters offer the best performance and flexibility.</span></span>
* <span data-ttu-id="7a11f-492">為了獲得最快速的插入效能，請遵循下列一般指導方針，但要針對您的案例進行測試：</span><span class="sxs-lookup"><span data-stu-id="7a11f-492">For the fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="7a11f-493">如果 < 100 個資料列，使用單一參數化 INSERT 命令。</span><span class="sxs-lookup"><span data-stu-id="7a11f-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="7a11f-494">如果 < 1000 個資料列，使用資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="7a11f-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="7a11f-495">如果 >= 1000 個資料列，使用 SqlBulkCopy。</span><span class="sxs-lookup"><span data-stu-id="7a11f-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="7a11f-496">針對更新和刪除作業，使用資料表值參數搭配預存程序邏輯，決定要在資料表參數中每個資料列上執行的正確作業。</span><span class="sxs-lookup"><span data-stu-id="7a11f-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines the correct operation on each row in the table parameter.</span></span>
* <span data-ttu-id="7a11f-497">批次大小的指導方針：</span><span class="sxs-lookup"><span data-stu-id="7a11f-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="7a11f-498">使用符合您的應用程式和商務需求的最大批次大小。</span><span class="sxs-lookup"><span data-stu-id="7a11f-498">Use the largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="7a11f-499">在大型批次的效能提升和暫時性或災難性失敗的風險之間取得平衡。</span><span class="sxs-lookup"><span data-stu-id="7a11f-499">Balance the performance gain of large batches with the risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="7a11f-500">重試或在批次中遺失資料的後果是什麼？</span><span class="sxs-lookup"><span data-stu-id="7a11f-500">What is the consequence of retries or loss of the data in the batch?</span></span> 
  * <span data-ttu-id="7a11f-501">測試最大批次大小，確認 SQL Database 不會拒絕它。</span><span class="sxs-lookup"><span data-stu-id="7a11f-501">Test the largest batch size to verify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="7a11f-502">建立組態設定來控制批次處理，例如批次大小或緩衝時間範圍。</span><span class="sxs-lookup"><span data-stu-id="7a11f-502">Create configuration settings that control batching, such as the batch size or the buffering time window.</span></span> <span data-ttu-id="7a11f-503">這些設定提供彈性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-503">These settings provide flexibility.</span></span> <span data-ttu-id="7a11f-504">您可以在生產環境中變更批次處理行為，不需重新部署雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7a11f-504">You can change the batching behavior in production without redeploying the cloud service.</span></span>
* <span data-ttu-id="7a11f-505">避免在一個資料庫的單一資料表上平行執行批次。</span><span class="sxs-lookup"><span data-stu-id="7a11f-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="7a11f-506">如果您選擇將單一批次分成多個背景工作角色執行緒，請執行測試來決定理想的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="7a11f-506">If you do choose to divide a single batch across multiple worker threads, run tests to determine the ideal number of threads.</span></span> <span data-ttu-id="7a11f-507">超過未確定的臨界值之後，更多的執行緒只會降低效能，不會提高效能。</span><span class="sxs-lookup"><span data-stu-id="7a11f-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="7a11f-508">在更多案例下，考慮依大小和時間緩衝來實作批次處理。</span><span class="sxs-lookup"><span data-stu-id="7a11f-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a11f-509">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a11f-509">Next steps</span></span>
<span data-ttu-id="7a11f-510">這篇文章著重於與批次處理相關的資料庫設計和程式碼撰寫技術，如何改善應用程式的效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="7a11f-510">This article focused on how database design and coding techniques related to batching can improve your application performance and scalability.</span></span> <span data-ttu-id="7a11f-511">但這只是整體策略中的一個因素。</span><span class="sxs-lookup"><span data-stu-id="7a11f-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="7a11f-512">關於其他可改善效能和延展性的方式，請參閱[單一資料庫的 Azure SQL Database 效能指引](sql-database-performance-guidance.md)和[彈性集區的價格和效能考量](sql-database-elastic-pool-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="7a11f-512">For more ways to improve performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

