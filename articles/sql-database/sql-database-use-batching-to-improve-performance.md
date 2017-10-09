---
title: "aaaHow toouse 批次處理 tooimprove Azure SQL Database 應用程式效能"
description: "hello 主題提供辨識項，批次資料庫作業大幅 imroves hello 速度和 Azure SQL Database 應用程式的延展性。 雖然這些批次技術任何 SQL Server 資料庫運作，但 hello 的 hello 文章的焦點是在 Azure 上。"
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
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="284ea-104">如何 toouse 批次處理 tooimprove SQL Database 應用程式效能</span><span class="sxs-lookup"><span data-stu-id="284ea-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="284ea-105">批次處理作業 tooAzure SQL Database 會大幅改善 hello 效能和延展性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="284ea-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="284ea-106">順序 toounderstand hello 好處，在這篇文章 hello 第一個部分涵蓋比較循序和批次要求 tooa SQL Database 的一些範例測試結果。</span><span class="sxs-lookup"><span data-stu-id="284ea-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="284ea-107">hello hello 文章的其餘部分會顯示 hello 技術、 案例和考量 toohelp 您 toouse 批次已成功將 Azure 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="284ea-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="284ea-108">為什麼批次處理對 SQL Database 很重要？</span><span class="sxs-lookup"><span data-stu-id="284ea-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="284ea-109">呼叫 tooa 遠端服務的批次處理是已知的策略，提升效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="284ea-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="284ea-110">都那里固定的處理成本 tooany 互動與遠端服務，例如序列化、 網路傳輸和還原序列化。</span><span class="sxs-lookup"><span data-stu-id="284ea-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="284ea-111">將許多個別交易包裝成單一批次可將這些成本降到最低。</span><span class="sxs-lookup"><span data-stu-id="284ea-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="284ea-112">本文中，我們想要 tooexamine 各種 SQL Database 批次處理策略和案例。</span><span class="sxs-lookup"><span data-stu-id="284ea-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="284ea-113">雖然這些策略也是使用 SQL Server 的內部部署應用程式很重要的有多種原因所造成的反白顯示 hello 的批次處理使用 SQL Database:</span><span class="sxs-lookup"><span data-stu-id="284ea-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="284ea-114">沒有可能會比較高的網路延遲存取 SQL 資料庫，特別是如果您要從外部 hello 存取 SQL 資料庫相同的 Microsoft Azure 資料中心。</span><span class="sxs-lookup"><span data-stu-id="284ea-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="284ea-115">hello 多租用戶特性為 SQL 資料庫，表示 hello 效率的 hello 資料存取層相互關聯 toohello hello 資料庫的整體延展性。</span><span class="sxs-lookup"><span data-stu-id="284ea-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="284ea-116">SQL 資料庫必須防止任何單一租用戶/使用者獨佔資料庫資源 toohello 而妨礙其他租用戶。</span><span class="sxs-lookup"><span data-stu-id="284ea-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="284ea-117">在回應 toousage 超過預先定義的配額，SQL Database 可以減少輸送量或是以節流例外回應。</span><span class="sxs-lookup"><span data-stu-id="284ea-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="284ea-118">效率，例如，批次，可讓您 toodo 達到這些限制前於 SQL Database 的更多工作。</span><span class="sxs-lookup"><span data-stu-id="284ea-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="284ea-119">在使用多個資料庫 (分區化) 的架構下，批次處理也很有效益。</span><span class="sxs-lookup"><span data-stu-id="284ea-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="284ea-120">每個資料庫單元與您互動的 hello 效率仍然是整體延展性的關鍵因素。</span><span class="sxs-lookup"><span data-stu-id="284ea-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="284ea-121">使用 SQL Database hello 優點的其中一個是您不需要 toomanage hello 伺服器主機 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="284ea-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="284ea-122">不過，此受管理的基礎結構也表示您必須以不同方式的相關資料庫最佳化 toothink。</span><span class="sxs-lookup"><span data-stu-id="284ea-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="284ea-123">您可以不再尋找 tooimprove hello 資料庫硬體或網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="284ea-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="284ea-124">Microsoft Azure 會控制那些環境。</span><span class="sxs-lookup"><span data-stu-id="284ea-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="284ea-125">您可以控制 hello 主要區域是您的應用程式與 SQL Database 之間的互動方式。</span><span class="sxs-lookup"><span data-stu-id="284ea-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="284ea-126">批次處理屬於這些最佳化作法之一。</span><span class="sxs-lookup"><span data-stu-id="284ea-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="284ea-127">hello 紙張 hello 第一個部分會檢查.NET 應用程式使用 SQL Database 的各種批次技術。</span><span class="sxs-lookup"><span data-stu-id="284ea-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="284ea-128">hello 最後兩節討論批次處理方針和案例。</span><span class="sxs-lookup"><span data-stu-id="284ea-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="284ea-129">批次處理策略</span><span class="sxs-lookup"><span data-stu-id="284ea-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="284ea-130">有關本主題中計時結果的注意事項</span><span class="sxs-lookup"><span data-stu-id="284ea-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="284ea-131">結果並不是基準，目的只是 tooshow**相對效能**。</span><span class="sxs-lookup"><span data-stu-id="284ea-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="284ea-132">計時至少根據 10 個測試回合的平均值。</span><span class="sxs-lookup"><span data-stu-id="284ea-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="284ea-133">作業插入至空的資料表。</span><span class="sxs-lookup"><span data-stu-id="284ea-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="284ea-134">這些測試測量的 V12 之前，所以它們不一定對應使用 hello 新 V12 資料庫中，您可能會遇到的 toothroughput[服務層](sql-database-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="284ea-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="284ea-135">批次技術 hello hello 相對效益應該類似。</span><span class="sxs-lookup"><span data-stu-id="284ea-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="284ea-136">交易</span><span class="sxs-lookup"><span data-stu-id="284ea-136">Transactions</span></span>
<span data-ttu-id="284ea-137">似乎奇怪 toobegin 檢視討論交易批次處理。</span><span class="sxs-lookup"><span data-stu-id="284ea-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="284ea-138">但 hello 使用用戶端交易會對具有難以察覺的伺服器端批次處理效果，可改善效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="284ea-139">交易可以加入只幾行程式碼，讓使用者提供快速 tooimprove 循序作業效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="284ea-140">請考慮下列 C# 程式碼，其中包含一連串的 insert hello 和簡單的資料表上的 update 作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="284ea-141">hello 下列 ADO.NET 程式碼，以循序方式執行這些作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="284ea-142">hello 最佳方式 toooptimize 這段程式碼是 tooimplement 某種形式的用戶端批次處理這些呼叫。</span><span class="sxs-lookup"><span data-stu-id="284ea-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="284ea-143">但是 hello 序列呼叫包裝在交易中沒有簡單的方式 tooincrease hello 這個程式碼的效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="284ea-144">以下是 hello 相同的程式碼改成使用交易。</span><span class="sxs-lookup"><span data-stu-id="284ea-144">Here is hello same code that uses a transaction.</span></span>

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

<span data-ttu-id="284ea-145">這兩個範例實際上都使用交易。</span><span class="sxs-lookup"><span data-stu-id="284ea-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="284ea-146">在 hello 第一個範例中，每個個別的呼叫是隱含的交易。</span><span class="sxs-lookup"><span data-stu-id="284ea-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="284ea-147">在 hello 第二個範例中，明確的交易中包裝所有 hello 呼叫。</span><span class="sxs-lookup"><span data-stu-id="284ea-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="284ea-148">每個 hello 文件以 hello[預先寫入交易記錄檔](https://msdn.microsoft.com/library/ms186259.aspx)，hello 交易認可時，記錄檔記錄會排清的 toohello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="284ea-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="284ea-149">因此只要在交易中包含多個呼叫，hello 寫入 toohello 交易記錄檔可能會延遲 hello 交易認可之前。</span><span class="sxs-lookup"><span data-stu-id="284ea-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="284ea-150">作用中，您要啟用 hello 寫入 toohello 伺服器的交易記錄的批次。</span><span class="sxs-lookup"><span data-stu-id="284ea-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="284ea-151">hello 下表顯示一些臨機操作測試結果。</span><span class="sxs-lookup"><span data-stu-id="284ea-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="284ea-152">hello 相同循序插入與交易不會執行 hello 測試。</span><span class="sxs-lookup"><span data-stu-id="284ea-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="284ea-153">如需詳細的觀點來看，hello 第一組測試從遠端執行從膝上型電腦 toohello 資料庫在 Microsoft Azure 中。</span><span class="sxs-lookup"><span data-stu-id="284ea-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="284ea-154">hello 第二組測試從執行雲端服務和資料庫位在 hello 相同 Microsoft Azure 資料中心 （美國西部）。</span><span class="sxs-lookup"><span data-stu-id="284ea-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="284ea-155">hello 下表顯示 hello 持續時間以毫秒為單位的逾時或無交易的循序插入。</span><span class="sxs-lookup"><span data-stu-id="284ea-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="284ea-156">**在內部部署 tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="284ea-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="284ea-157">作業</span><span class="sxs-lookup"><span data-stu-id="284ea-157">Operations</span></span> | <span data-ttu-id="284ea-158">無交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-158">No Transaction (ms)</span></span> | <span data-ttu-id="284ea-159">交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="284ea-160">1</span><span class="sxs-lookup"><span data-stu-id="284ea-160">1</span></span> |<span data-ttu-id="284ea-161">130</span><span class="sxs-lookup"><span data-stu-id="284ea-161">130</span></span> |<span data-ttu-id="284ea-162">402</span><span class="sxs-lookup"><span data-stu-id="284ea-162">402</span></span> |
| <span data-ttu-id="284ea-163">10</span><span class="sxs-lookup"><span data-stu-id="284ea-163">10</span></span> |<span data-ttu-id="284ea-164">1208</span><span class="sxs-lookup"><span data-stu-id="284ea-164">1208</span></span> |<span data-ttu-id="284ea-165">1226</span><span class="sxs-lookup"><span data-stu-id="284ea-165">1226</span></span> |
| <span data-ttu-id="284ea-166">100</span><span class="sxs-lookup"><span data-stu-id="284ea-166">100</span></span> |<span data-ttu-id="284ea-167">12662</span><span class="sxs-lookup"><span data-stu-id="284ea-167">12662</span></span> |<span data-ttu-id="284ea-168">10395</span><span class="sxs-lookup"><span data-stu-id="284ea-168">10395</span></span> |
| <span data-ttu-id="284ea-169">1000</span><span class="sxs-lookup"><span data-stu-id="284ea-169">1000</span></span> |<span data-ttu-id="284ea-170">128852</span><span class="sxs-lookup"><span data-stu-id="284ea-170">128852</span></span> |<span data-ttu-id="284ea-171">102917</span><span class="sxs-lookup"><span data-stu-id="284ea-171">102917</span></span> |

<span data-ttu-id="284ea-172">**Azure tooAzure （相同資料中心）**:</span><span class="sxs-lookup"><span data-stu-id="284ea-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="284ea-173">作業</span><span class="sxs-lookup"><span data-stu-id="284ea-173">Operations</span></span> | <span data-ttu-id="284ea-174">無交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-174">No Transaction (ms)</span></span> | <span data-ttu-id="284ea-175">交易 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="284ea-176">1</span><span class="sxs-lookup"><span data-stu-id="284ea-176">1</span></span> |<span data-ttu-id="284ea-177">21</span><span class="sxs-lookup"><span data-stu-id="284ea-177">21</span></span> |<span data-ttu-id="284ea-178">26</span><span class="sxs-lookup"><span data-stu-id="284ea-178">26</span></span> |
| <span data-ttu-id="284ea-179">10</span><span class="sxs-lookup"><span data-stu-id="284ea-179">10</span></span> |<span data-ttu-id="284ea-180">220</span><span class="sxs-lookup"><span data-stu-id="284ea-180">220</span></span> |<span data-ttu-id="284ea-181">56</span><span class="sxs-lookup"><span data-stu-id="284ea-181">56</span></span> |
| <span data-ttu-id="284ea-182">100</span><span class="sxs-lookup"><span data-stu-id="284ea-182">100</span></span> |<span data-ttu-id="284ea-183">2145</span><span class="sxs-lookup"><span data-stu-id="284ea-183">2145</span></span> |<span data-ttu-id="284ea-184">341</span><span class="sxs-lookup"><span data-stu-id="284ea-184">341</span></span> |
| <span data-ttu-id="284ea-185">1000</span><span class="sxs-lookup"><span data-stu-id="284ea-185">1000</span></span> |<span data-ttu-id="284ea-186">21479</span><span class="sxs-lookup"><span data-stu-id="284ea-186">21479</span></span> |<span data-ttu-id="284ea-187">2756</span><span class="sxs-lookup"><span data-stu-id="284ea-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="284ea-188">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="284ea-188">Results are not benchmarks.</span></span> <span data-ttu-id="284ea-189">請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="284ea-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="284ea-190">根據 hello 先前的測試結果，將單一作業包裝在交易中其實會降低效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="284ea-191">但隨著您增加 hello 在單一交易中的作業數目時，會變成更標示 hello 效能改進。</span><span class="sxs-lookup"><span data-stu-id="284ea-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="284ea-192">hello Microsoft Azure 資料中心內發生的所有作業時，也更明顯 hello 效能差異。</span><span class="sxs-lookup"><span data-stu-id="284ea-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="284ea-193">hello 使用從外部 hello Microsoft Azure 資料中心的 SQL Database 的延遲增加減低使用交易所 hello 效能提升。</span><span class="sxs-lookup"><span data-stu-id="284ea-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="284ea-194">雖然 hello 使用交易可以提高效能，繼續太[觀察交易和連接的最佳作法](https://msdn.microsoft.com/library/ms187484.aspx)。</span><span class="sxs-lookup"><span data-stu-id="284ea-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="284ea-195">Hello 工作完成後，請保留 hello 交易越短越好，並關閉 hello 資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="284ea-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="284ea-196">hello hello 前一個範例中使用陳述式可確保 hello 連接已關閉時完成 hello 後續程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="284ea-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="284ea-197">hello 前一個範例示範您可以加入本機交易 tooany ADO.NET 程式碼透過兩行。</span><span class="sxs-lookup"><span data-stu-id="284ea-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="284ea-198">交易提供快速的方式，tooimprove hello 效能的程式碼，可循序插入、 更新和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="284ea-199">不過，為了 hello 最快效能，請考慮變更 hello 程式碼進一步 tootake 用戶端批次的優點，例如資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="284ea-200">如需 ADO.NET 中的交易的詳細資訊，請參閱 [ADO.NET 中的本機交易](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions)。</span><span class="sxs-lookup"><span data-stu-id="284ea-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="284ea-201">資料表值參數</span><span class="sxs-lookup"><span data-stu-id="284ea-201">Table-valued parameters</span></span>
<span data-ttu-id="284ea-202">資料表值參數支援使用者定義資料表類型做為 Transact-SQL 陳述式、預存程序和函數中的參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="284ea-203">此用戶端批次處理技術可讓您 toosend 內 hello 資料表值參數資料的多個資料列。</span><span class="sxs-lookup"><span data-stu-id="284ea-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="284ea-204">toouse 資料表值參數，會先定義資料表類型。</span><span class="sxs-lookup"><span data-stu-id="284ea-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="284ea-205">hello 下列 TRANSACT-SQL 陳述式建立資料表類型名為**MyTableType**。</span><span class="sxs-lookup"><span data-stu-id="284ea-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="284ea-206">在程式碼中，您會建立**DataTable**以 hello 完全相同的名稱和類型的 hello 資料表類型。</span><span class="sxs-lookup"><span data-stu-id="284ea-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="284ea-207">將這個 **DataTable** 傳入文字查詢或預存程序呼叫中的參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="284ea-208">hello 下例示範這項技術：</span><span class="sxs-lookup"><span data-stu-id="284ea-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
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

<span data-ttu-id="284ea-209">Hello 上述範例中，在 hello **SqlCommand**物件是資料表值參數，會將資料列 **@TestTvp** 。</span><span class="sxs-lookup"><span data-stu-id="284ea-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="284ea-210">先前建立的 hello **DataTable** hello toothis 參數指派給物件**SqlCommand.Parameters.Add**方法。</span><span class="sxs-lookup"><span data-stu-id="284ea-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="284ea-211">批次處理 hello 插入其中一個呼叫會大幅增加 hello 效能比循序插入。</span><span class="sxs-lookup"><span data-stu-id="284ea-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="284ea-212">tooimprove hello 前一個範例，會使用預存程序，而不是以文字為基礎的命令。</span><span class="sxs-lookup"><span data-stu-id="284ea-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="284ea-213">hello 下列 TRANSACT-SQL 命令建立預存程序採用 hello **SimpleTestTableType**資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="284ea-214">然後變更 hello **SqlCommand** hello 前一個範例 toohello 後面的程式碼中宣告的物件。</span><span class="sxs-lookup"><span data-stu-id="284ea-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="284ea-215">在大部分情況下，資料表值參數的效能同於或高於其他批次處理技術。</span><span class="sxs-lookup"><span data-stu-id="284ea-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="284ea-216">資料表值參數通常較適合，因為比其他選項更有彈性。</span><span class="sxs-lookup"><span data-stu-id="284ea-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="284ea-217">例如，SQL 大量複製等其他技術只允許 hello 插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="284ea-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="284ea-218">但使用資料表值參數，您可以使用邏輯在 hello 預存程序 toodetermine 哪些資料列會更新和插入。</span><span class="sxs-lookup"><span data-stu-id="284ea-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="284ea-219">hello 資料表類型也可以修改的 toocontain 表示 hello 指定資料列應該是插入、 更新或刪除的 「 作業 」 資料行。</span><span class="sxs-lookup"><span data-stu-id="284ea-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="284ea-220">下表中的 hello 顯示 hello 使用資料表值參數的臨機操作測試結果，以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="284ea-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="284ea-221">作業</span><span class="sxs-lookup"><span data-stu-id="284ea-221">Operations</span></span> | <span data-ttu-id="284ea-222">在內部部署 tooAzure （毫秒）</span><span class="sxs-lookup"><span data-stu-id="284ea-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="284ea-223">Azure 相同資料中心 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="284ea-224">1</span><span class="sxs-lookup"><span data-stu-id="284ea-224">1</span></span> |<span data-ttu-id="284ea-225">124</span><span class="sxs-lookup"><span data-stu-id="284ea-225">124</span></span> |<span data-ttu-id="284ea-226">32</span><span class="sxs-lookup"><span data-stu-id="284ea-226">32</span></span> |
| <span data-ttu-id="284ea-227">10</span><span class="sxs-lookup"><span data-stu-id="284ea-227">10</span></span> |<span data-ttu-id="284ea-228">131</span><span class="sxs-lookup"><span data-stu-id="284ea-228">131</span></span> |<span data-ttu-id="284ea-229">25</span><span class="sxs-lookup"><span data-stu-id="284ea-229">25</span></span> |
| <span data-ttu-id="284ea-230">100</span><span class="sxs-lookup"><span data-stu-id="284ea-230">100</span></span> |<span data-ttu-id="284ea-231">338</span><span class="sxs-lookup"><span data-stu-id="284ea-231">338</span></span> |<span data-ttu-id="284ea-232">51</span><span class="sxs-lookup"><span data-stu-id="284ea-232">51</span></span> |
| <span data-ttu-id="284ea-233">1000</span><span class="sxs-lookup"><span data-stu-id="284ea-233">1000</span></span> |<span data-ttu-id="284ea-234">2615</span><span class="sxs-lookup"><span data-stu-id="284ea-234">2615</span></span> |<span data-ttu-id="284ea-235">382</span><span class="sxs-lookup"><span data-stu-id="284ea-235">382</span></span> |
| <span data-ttu-id="284ea-236">10000</span><span class="sxs-lookup"><span data-stu-id="284ea-236">10000</span></span> |<span data-ttu-id="284ea-237">23830</span><span class="sxs-lookup"><span data-stu-id="284ea-237">23830</span></span> |<span data-ttu-id="284ea-238">3586</span><span class="sxs-lookup"><span data-stu-id="284ea-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="284ea-239">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="284ea-239">Results are not benchmarks.</span></span> <span data-ttu-id="284ea-240">請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="284ea-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="284ea-241">從批次的 hello 效能提升會立即出現。</span><span class="sxs-lookup"><span data-stu-id="284ea-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="284ea-242">在上一個循序測試 hello，1000 次作業花費 129 秒外部 hello 資料中心和從 hello 資料中心內的 21 秒。</span><span class="sxs-lookup"><span data-stu-id="284ea-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="284ea-243">但是使用資料表值參數，1000 次作業會採用只有 2.6 秒 hello 資料中心以外和 hello 資料中心內則只需 0.4 秒。</span><span class="sxs-lookup"><span data-stu-id="284ea-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="284ea-244">如需資料表值參數的詳細資訊，請參閱 [資料表值參數](https://msdn.microsoft.com/library/bb510489.aspx)。</span><span class="sxs-lookup"><span data-stu-id="284ea-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="284ea-245">SQL 大量複製</span><span class="sxs-lookup"><span data-stu-id="284ea-245">SQL bulk copy</span></span>
<span data-ttu-id="284ea-246">SQL 大量複製是另一個方式 tooinsert 大量資料到目標資料庫。</span><span class="sxs-lookup"><span data-stu-id="284ea-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="284ea-247">.NET 應用程式可以使用 hello **SqlBulkCopy**類別 tooperform 大量插入作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="284ea-248">**SqlBulkCopy**函式 toohello 命令列工具，在類似**Bcp.exe**，或使用 TRANSACT-SQL 陳述式，hello **BULK INSERT**。</span><span class="sxs-lookup"><span data-stu-id="284ea-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="284ea-249">hello 下列程式碼範例示範 toobulk 複製 hello hello 來源中的資料列**DataTable**，資料表、 在 SQL Server，MyTable toohello 目的地資料表。</span><span class="sxs-lookup"><span data-stu-id="284ea-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

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

<span data-ttu-id="284ea-250">在某些情況下，大量複製比資料表值參數更適合。</span><span class="sxs-lookup"><span data-stu-id="284ea-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="284ea-251">請參閱資料表值參數與 BULK INSERT 作業 hello 主題中的 hello 比較表[資料表值參數](https://msdn.microsoft.com/library/bb510489.aspx)。</span><span class="sxs-lookup"><span data-stu-id="284ea-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="284ea-252">hello 下列臨機操作測試結果顯示 hello 效能與批次處理**SqlBulkCopy**以毫秒為單位。</span><span class="sxs-lookup"><span data-stu-id="284ea-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="284ea-253">作業</span><span class="sxs-lookup"><span data-stu-id="284ea-253">Operations</span></span> | <span data-ttu-id="284ea-254">在內部部署 tooAzure （毫秒）</span><span class="sxs-lookup"><span data-stu-id="284ea-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="284ea-255">Azure 相同資料中心 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="284ea-256">1</span><span class="sxs-lookup"><span data-stu-id="284ea-256">1</span></span> |<span data-ttu-id="284ea-257">433</span><span class="sxs-lookup"><span data-stu-id="284ea-257">433</span></span> |<span data-ttu-id="284ea-258">57</span><span class="sxs-lookup"><span data-stu-id="284ea-258">57</span></span> |
| <span data-ttu-id="284ea-259">10</span><span class="sxs-lookup"><span data-stu-id="284ea-259">10</span></span> |<span data-ttu-id="284ea-260">441</span><span class="sxs-lookup"><span data-stu-id="284ea-260">441</span></span> |<span data-ttu-id="284ea-261">32</span><span class="sxs-lookup"><span data-stu-id="284ea-261">32</span></span> |
| <span data-ttu-id="284ea-262">100</span><span class="sxs-lookup"><span data-stu-id="284ea-262">100</span></span> |<span data-ttu-id="284ea-263">636</span><span class="sxs-lookup"><span data-stu-id="284ea-263">636</span></span> |<span data-ttu-id="284ea-264">53</span><span class="sxs-lookup"><span data-stu-id="284ea-264">53</span></span> |
| <span data-ttu-id="284ea-265">1000</span><span class="sxs-lookup"><span data-stu-id="284ea-265">1000</span></span> |<span data-ttu-id="284ea-266">2535</span><span class="sxs-lookup"><span data-stu-id="284ea-266">2535</span></span> |<span data-ttu-id="284ea-267">341</span><span class="sxs-lookup"><span data-stu-id="284ea-267">341</span></span> |
| <span data-ttu-id="284ea-268">10000</span><span class="sxs-lookup"><span data-stu-id="284ea-268">10000</span></span> |<span data-ttu-id="284ea-269">21605</span><span class="sxs-lookup"><span data-stu-id="284ea-269">21605</span></span> |<span data-ttu-id="284ea-270">2737</span><span class="sxs-lookup"><span data-stu-id="284ea-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="284ea-271">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="284ea-271">Results are not benchmarks.</span></span> <span data-ttu-id="284ea-272">請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="284ea-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="284ea-273">在較小的批次大小 hello 使用資料表值參數的效能勝過 hello **SqlBulkCopy**類別。</span><span class="sxs-lookup"><span data-stu-id="284ea-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="284ea-274">不過， **SqlBulkCopy** hello 測試 1,000 和 10,000 個資料列的執行速度比資料表值參數 12-31%。</span><span class="sxs-lookup"><span data-stu-id="284ea-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="284ea-275">例如資料表值參數， **SqlBulkCopy**是不錯的選項，批次的插入，尤其是與 toohello 效能的非批次作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="284ea-276">如需 ADO.NET 中的大量複製的詳細資訊，請參閱 [SQL Server 中的大量複製作業](https://msdn.microsoft.com/library/7ek5da1a.aspx)。</span><span class="sxs-lookup"><span data-stu-id="284ea-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="284ea-277">多資料列參數化 INSERT 陳述式</span><span class="sxs-lookup"><span data-stu-id="284ea-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="284ea-278">小批次的一種替代方法是 tooconstruct 大型參數化 INSERT 陳述式會插入多個資料列。</span><span class="sxs-lookup"><span data-stu-id="284ea-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="284ea-279">hello，下列程式碼範例示範這項技術。</span><span class="sxs-lookup"><span data-stu-id="284ea-279">hello following code example demonstrates this technique.</span></span>

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


<span data-ttu-id="284ea-280">此範例的目的在於 tooshow hello 基本概念。</span><span class="sxs-lookup"><span data-stu-id="284ea-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="284ea-281">比較真實的案例會同時循環所需的 hello 實體 tooconstruct hello 查詢字串和 hello 命令參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="284ea-282">最多只能 tooa 2100 查詢參數，因此這會限制 hello 總數，這種方式可以處理的資料列的總數。</span><span class="sxs-lookup"><span data-stu-id="284ea-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="284ea-283">下列臨機操作測試結果顯示 hello 效能這種類型的 insert 陳述式，以毫秒為單位的 hello。</span><span class="sxs-lookup"><span data-stu-id="284ea-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="284ea-284">作業</span><span class="sxs-lookup"><span data-stu-id="284ea-284">Operations</span></span> | <span data-ttu-id="284ea-285">資料表值參數 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="284ea-286">單一陳述式 INSERT (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="284ea-287">1</span><span class="sxs-lookup"><span data-stu-id="284ea-287">1</span></span> |<span data-ttu-id="284ea-288">32</span><span class="sxs-lookup"><span data-stu-id="284ea-288">32</span></span> |<span data-ttu-id="284ea-289">20</span><span class="sxs-lookup"><span data-stu-id="284ea-289">20</span></span> |
| <span data-ttu-id="284ea-290">10</span><span class="sxs-lookup"><span data-stu-id="284ea-290">10</span></span> |<span data-ttu-id="284ea-291">30</span><span class="sxs-lookup"><span data-stu-id="284ea-291">30</span></span> |<span data-ttu-id="284ea-292">25</span><span class="sxs-lookup"><span data-stu-id="284ea-292">25</span></span> |
| <span data-ttu-id="284ea-293">100</span><span class="sxs-lookup"><span data-stu-id="284ea-293">100</span></span> |<span data-ttu-id="284ea-294">33</span><span class="sxs-lookup"><span data-stu-id="284ea-294">33</span></span> |<span data-ttu-id="284ea-295">51</span><span class="sxs-lookup"><span data-stu-id="284ea-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="284ea-296">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="284ea-296">Results are not benchmarks.</span></span> <span data-ttu-id="284ea-297">請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="284ea-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="284ea-298">如果批次少於 100 的資料列，這種方法會稍微快一些。</span><span class="sxs-lookup"><span data-stu-id="284ea-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="284ea-299">雖然 hello 改進很小，這項技術是另一個選項，可能也在特定應用程式案例中運作。</span><span class="sxs-lookup"><span data-stu-id="284ea-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="284ea-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="284ea-300">DataAdapter</span></span>
<span data-ttu-id="284ea-301">hello **DataAdapter**類別可讓您 toomodify**資料集**物件，然後送出 hello 變更做為 INSERT、 UPDATE 和 DELETE 作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="284ea-302">如果您使用 hello **DataAdapter**在這種方式，是很重要，個別呼叫 toonote 會針對每個相異的作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="284ea-303">tooimprove 效能，使用 hello **UpdateBatchSize**屬性 toohello 數目應該同時批次處理的作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="284ea-304">如需詳細資訊，請參閱 [使用 Dataadapter 執行批次作業](https://msdn.microsoft.com/library/aadf8fk2.aspx)。</span><span class="sxs-lookup"><span data-stu-id="284ea-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="284ea-305">Entity Framework</span><span class="sxs-lookup"><span data-stu-id="284ea-305">Entity framework</span></span>
<span data-ttu-id="284ea-306">Entity Framework 目前不支援批次處理。</span><span class="sxs-lookup"><span data-stu-id="284ea-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="284ea-307">Hello 社群中的不同開發人員嘗試 toodemonstrate 因應措施，例如覆寫 hello **SaveChanges**方法。</span><span class="sxs-lookup"><span data-stu-id="284ea-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="284ea-308">但 hello 解決方案通常 toohello 複雜和自訂應用程式和資料模型。</span><span class="sxs-lookup"><span data-stu-id="284ea-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="284ea-309">hello Entity Framework codeplex 專案目前沒有這項功能要求上的討論頁。</span><span class="sxs-lookup"><span data-stu-id="284ea-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="284ea-310">tooview 本討論中，請參閱[設計會議記錄-2012 年 8 月 2 日](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012)。</span><span class="sxs-lookup"><span data-stu-id="284ea-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="284ea-311">XML</span><span class="sxs-lookup"><span data-stu-id="284ea-311">XML</span></span>
<span data-ttu-id="284ea-312">為求完整起見，我們覺得很重要的 tootalk xml 做為批次策略。</span><span class="sxs-lookup"><span data-stu-id="284ea-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="284ea-313">不過，hello 使用 XML 沒有任何優於其他方法和幾個缺點。</span><span class="sxs-lookup"><span data-stu-id="284ea-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="284ea-314">hello 方法是類似 tootable 值的參數，但 XML 檔案，或是字串傳遞 tooa 預存程序，而不是使用者定義的資料表。</span><span class="sxs-lookup"><span data-stu-id="284ea-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="284ea-315">hello 預存程序會剖析 hello 預存程序中的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="284ea-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="284ea-316">Toothis 方法有幾個缺點：</span><span class="sxs-lookup"><span data-stu-id="284ea-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="284ea-317">處理 XML 很麻煩又容易出錯。</span><span class="sxs-lookup"><span data-stu-id="284ea-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="284ea-318">剖析 hello XML hello 資料庫上的可能需要大量 CPU。</span><span class="sxs-lookup"><span data-stu-id="284ea-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="284ea-319">在大部分情況下，這種方法比資料表值參數更慢。</span><span class="sxs-lookup"><span data-stu-id="284ea-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="284ea-320">基於這些理由，不建議 hello 使用 XML 進行批次查詢。</span><span class="sxs-lookup"><span data-stu-id="284ea-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="284ea-321">批次處理考量</span><span class="sxs-lookup"><span data-stu-id="284ea-321">Batching considerations</span></span>
<span data-ttu-id="284ea-322">hello 下列各節提供 hello 使用批次作業中 SQL Database 應用程式的詳細指引。</span><span class="sxs-lookup"><span data-stu-id="284ea-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="284ea-323">權衡取捨</span><span class="sxs-lookup"><span data-stu-id="284ea-323">Tradeoffs</span></span>
<span data-ttu-id="284ea-324">根據您的架構而定，批次處理可能需要在效能和恢復功能之間有所取捨。</span><span class="sxs-lookup"><span data-stu-id="284ea-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="284ea-325">例如，請考慮 hello 案例中，您的角色異常中斷。</span><span class="sxs-lookup"><span data-stu-id="284ea-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="284ea-326">如果您遺失一個資料列，hello 影響會小於遺失大批尚未認可的資料列的大型批次的 hello 影響。</span><span class="sxs-lookup"><span data-stu-id="284ea-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="284ea-327">當您在指定的時段傳送 toohello 資料庫之前，先緩衝處理資料列時，沒有更大的風險。</span><span class="sxs-lookup"><span data-stu-id="284ea-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="284ea-328">這些權衡取捨，因為評估您要批次處理 hello 的作業類型。</span><span class="sxs-lookup"><span data-stu-id="284ea-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="284ea-329">對於較不重要的資料，應該更積極地批次處理 (較大的批次和較長的時間範圍)。</span><span class="sxs-lookup"><span data-stu-id="284ea-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="284ea-330">批次大小</span><span class="sxs-lookup"><span data-stu-id="284ea-330">Batch size</span></span>
<span data-ttu-id="284ea-331">在我們的測試時通常不利用 toobreaking 大型批次分成小塊。</span><span class="sxs-lookup"><span data-stu-id="284ea-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="284ea-332">事實上，這樣分割通常會導致效能比提交單一大型批次更慢。</span><span class="sxs-lookup"><span data-stu-id="284ea-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="284ea-333">例如，假設您想要 tooinsert 1000 個資料列。</span><span class="sxs-lookup"><span data-stu-id="284ea-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="284ea-334">hello 下表顯示要花多久 toouse 資料表值參數 tooinsert 1000 列分成較小的批次時。</span><span class="sxs-lookup"><span data-stu-id="284ea-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="284ea-335">批次大小</span><span class="sxs-lookup"><span data-stu-id="284ea-335">Batch size</span></span> | <span data-ttu-id="284ea-336">反覆運算次數</span><span class="sxs-lookup"><span data-stu-id="284ea-336">Iterations</span></span> | <span data-ttu-id="284ea-337">資料表值參數 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="284ea-338">1000</span><span class="sxs-lookup"><span data-stu-id="284ea-338">1000</span></span> |<span data-ttu-id="284ea-339">1</span><span class="sxs-lookup"><span data-stu-id="284ea-339">1</span></span> |<span data-ttu-id="284ea-340">347</span><span class="sxs-lookup"><span data-stu-id="284ea-340">347</span></span> |
| <span data-ttu-id="284ea-341">500</span><span class="sxs-lookup"><span data-stu-id="284ea-341">500</span></span> |<span data-ttu-id="284ea-342">2</span><span class="sxs-lookup"><span data-stu-id="284ea-342">2</span></span> |<span data-ttu-id="284ea-343">355</span><span class="sxs-lookup"><span data-stu-id="284ea-343">355</span></span> |
| <span data-ttu-id="284ea-344">100</span><span class="sxs-lookup"><span data-stu-id="284ea-344">100</span></span> |<span data-ttu-id="284ea-345">10</span><span class="sxs-lookup"><span data-stu-id="284ea-345">10</span></span> |<span data-ttu-id="284ea-346">465</span><span class="sxs-lookup"><span data-stu-id="284ea-346">465</span></span> |
| <span data-ttu-id="284ea-347">50</span><span class="sxs-lookup"><span data-stu-id="284ea-347">50</span></span> |<span data-ttu-id="284ea-348">20</span><span class="sxs-lookup"><span data-stu-id="284ea-348">20</span></span> |<span data-ttu-id="284ea-349">630</span><span class="sxs-lookup"><span data-stu-id="284ea-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="284ea-350">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="284ea-350">Results are not benchmarks.</span></span> <span data-ttu-id="284ea-351">請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="284ea-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="284ea-352">您可以看見 hello 1000 個資料列的最佳效能是 toosubmit 它們一次。</span><span class="sxs-lookup"><span data-stu-id="284ea-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="284ea-353">在其他測試中 （此處未顯示） 時發生輕微的效能改善 toobreak 10000 的資料列批次分成兩個批次為 5000。</span><span class="sxs-lookup"><span data-stu-id="284ea-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="284ea-354">但這些測試的 hello 資料表結構描述相當簡單，所以您必須執行上測試您的特定資料和批次大小 tooverify 這些研究結果。</span><span class="sxs-lookup"><span data-stu-id="284ea-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="284ea-355">另一個因素 tooconsider 是 hello 總批次變得太大，如果 SQL 資料庫可能會節流並拒絕 toocommit hello 批次。</span><span class="sxs-lookup"><span data-stu-id="284ea-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="284ea-356">Hello 獲得最佳結果，測試特定案例 toodetermine，如果沒有理想的批次大小。</span><span class="sxs-lookup"><span data-stu-id="284ea-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="284ea-357">請根據效能或錯誤的執行階段 tooenable 快速調整設定 hello 批次大小。</span><span class="sxs-lookup"><span data-stu-id="284ea-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="284ea-358">最後，平衡 hello hello 批次大小與 hello 與批次處理風險。</span><span class="sxs-lookup"><span data-stu-id="284ea-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="284ea-359">如果暫時性錯誤或 hello 角色失敗，請考慮 hello 或 hello hello 批次中的資料遺失的重試 hello 作業的結果。</span><span class="sxs-lookup"><span data-stu-id="284ea-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="284ea-360">平行處理</span><span class="sxs-lookup"><span data-stu-id="284ea-360">Parallel processing</span></span>
<span data-ttu-id="284ea-361">如果您 hello 方式減少 hello 批次大小，而使用多個執行緒 tooexecute hello 工作？</span><span class="sxs-lookup"><span data-stu-id="284ea-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="284ea-362">同樣地，我們的測試指出數個較小的多執行緒批次通常表現得比單一大型批次更差。</span><span class="sxs-lookup"><span data-stu-id="284ea-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="284ea-363">hello 下列測試嘗試 tooinsert 1000 個資料列中一個或多個平行批次。</span><span class="sxs-lookup"><span data-stu-id="284ea-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="284ea-364">此測試指出同時有多個批次實際上會降低效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="284ea-365">批次大小 [反覆運算次數]</span><span class="sxs-lookup"><span data-stu-id="284ea-365">Batch size [Iterations]</span></span> | <span data-ttu-id="284ea-366">兩個執行緒 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-366">Two threads (ms)</span></span> | <span data-ttu-id="284ea-367">四個執行緒 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-367">Four threads (ms)</span></span> | <span data-ttu-id="284ea-368">六個執行緒 (毫秒)</span><span class="sxs-lookup"><span data-stu-id="284ea-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="284ea-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="284ea-369">1000 [1]</span></span> |<span data-ttu-id="284ea-370">277</span><span class="sxs-lookup"><span data-stu-id="284ea-370">277</span></span> |<span data-ttu-id="284ea-371">315</span><span class="sxs-lookup"><span data-stu-id="284ea-371">315</span></span> |<span data-ttu-id="284ea-372">266</span><span class="sxs-lookup"><span data-stu-id="284ea-372">266</span></span> |
| <span data-ttu-id="284ea-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="284ea-373">500 [2]</span></span> |<span data-ttu-id="284ea-374">548</span><span class="sxs-lookup"><span data-stu-id="284ea-374">548</span></span> |<span data-ttu-id="284ea-375">278</span><span class="sxs-lookup"><span data-stu-id="284ea-375">278</span></span> |<span data-ttu-id="284ea-376">256</span><span class="sxs-lookup"><span data-stu-id="284ea-376">256</span></span> |
| <span data-ttu-id="284ea-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="284ea-377">250 [4]</span></span> |<span data-ttu-id="284ea-378">405</span><span class="sxs-lookup"><span data-stu-id="284ea-378">405</span></span> |<span data-ttu-id="284ea-379">329</span><span class="sxs-lookup"><span data-stu-id="284ea-379">329</span></span> |<span data-ttu-id="284ea-380">265</span><span class="sxs-lookup"><span data-stu-id="284ea-380">265</span></span> |
| <span data-ttu-id="284ea-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="284ea-381">100 [10]</span></span> |<span data-ttu-id="284ea-382">488</span><span class="sxs-lookup"><span data-stu-id="284ea-382">488</span></span> |<span data-ttu-id="284ea-383">439</span><span class="sxs-lookup"><span data-stu-id="284ea-383">439</span></span> |<span data-ttu-id="284ea-384">391</span><span class="sxs-lookup"><span data-stu-id="284ea-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="284ea-385">結果並不是基準。</span><span class="sxs-lookup"><span data-stu-id="284ea-385">Results are not benchmarks.</span></span> <span data-ttu-id="284ea-386">請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。</span><span class="sxs-lookup"><span data-stu-id="284ea-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="284ea-387">有 hello 效能降低的原因可能到期 tooparallelism:</span><span class="sxs-lookup"><span data-stu-id="284ea-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="284ea-388">同時有多個網路呼叫，而不只一個。</span><span class="sxs-lookup"><span data-stu-id="284ea-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="284ea-389">對單一資料表執行多個作業會導致爭用和鎖定。</span><span class="sxs-lookup"><span data-stu-id="284ea-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="284ea-390">多執行緒處理會引起額外負荷。</span><span class="sxs-lookup"><span data-stu-id="284ea-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="284ea-391">開啟多個連接的 hello 費用超過 hello 平行處理的效益。</span><span class="sxs-lookup"><span data-stu-id="284ea-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="284ea-392">如果您以不同的資料表或資料庫目標，則可能 toosee 這項策略而提升的一些效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="284ea-393">資料庫分區化或同盟就是適合這種方法的案例。</span><span class="sxs-lookup"><span data-stu-id="284ea-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="284ea-394">多個資料庫與路由不同資料 tooeach 資料庫，則會使用分區化。</span><span class="sxs-lookup"><span data-stu-id="284ea-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="284ea-395">如果每個小的批次即將 tooa 不同的資料庫，然後以平行方式執行 hello 作業可能會更有效率。</span><span class="sxs-lookup"><span data-stu-id="284ea-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="284ea-396">不過，hello 獲得效能未明顯 toouse 決策 toouse 資料庫分區化方案中的 hello 基礎。</span><span class="sxs-lookup"><span data-stu-id="284ea-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="284ea-397">在某些設計中，平行執行較小的批次可以在負載不足的系統中改善要求輸送量。</span><span class="sxs-lookup"><span data-stu-id="284ea-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="284ea-398">在此情況下，即使它是快速 tooprocess 單一較大的批次時，處理多個批次，以平行方式可能會更有效率。</span><span class="sxs-lookup"><span data-stu-id="284ea-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="284ea-399">如果您使用平行執行，請考慮控制 hello 最大工作者執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="284ea-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="284ea-400">數量較少可以減少爭用，並加快執行時間。</span><span class="sxs-lookup"><span data-stu-id="284ea-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="284ea-401">此外，請考慮 hello 這會在連接和交易 hello 目標資料庫的額外負載。</span><span class="sxs-lookup"><span data-stu-id="284ea-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="284ea-402">相關的效能因素</span><span class="sxs-lookup"><span data-stu-id="284ea-402">Related performance factors</span></span>
<span data-ttu-id="284ea-403">資料庫效能的一般指引也會影響批次處理。</span><span class="sxs-lookup"><span data-stu-id="284ea-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="284ea-404">例如，如果資料表具有大型的主索引鍵或許多非叢集索引，插入效能會降低。</span><span class="sxs-lookup"><span data-stu-id="284ea-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="284ea-405">如果資料表值參數使用預存程序，您可以使用 hello 命令**SET NOCOUNT ON** hello 程序的 hello 開頭。</span><span class="sxs-lookup"><span data-stu-id="284ea-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="284ea-406">這個陳述式會隱藏 hello 傳回 hello hello 程序中的 hello 受影響的資料列計數。</span><span class="sxs-lookup"><span data-stu-id="284ea-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="284ea-407">不過，在我們的測試，hello 使用**SET NOCOUNT ON**可能是沒有任何作用或是會降低效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="284ea-408">hello 測試預存程序很簡單，只有單一**插入**命令從 hello 資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="284ea-409">此陳述式可能有益於更複雜的預存程序。</span><span class="sxs-lookup"><span data-stu-id="284ea-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="284ea-410">但是，請勿假設該新增**SET NOCOUNT ON** tooyour 預存程序會自動改善效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="284ea-411">toounderstand hello 效果，請測試預存程序逾時或無 hello **SET NOCOUNT ON**陳述式。</span><span class="sxs-lookup"><span data-stu-id="284ea-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="284ea-412">批次處理案例</span><span class="sxs-lookup"><span data-stu-id="284ea-412">Batching scenarios</span></span>
<span data-ttu-id="284ea-413">hello 下列各節說明如何在三個應用程式案例 toouse 資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="284ea-414">hello 第一個案例示範緩衝和批次處理可以運作方式在一起。</span><span class="sxs-lookup"><span data-stu-id="284ea-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="284ea-415">hello 第二個案例會執行單一預存程序呼叫中的主檔/明細作業，以提高效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="284ea-416">hello 最後一個案例示範如何在 「 更新插入 」 作業中的 toouse 資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="284ea-417">緩衝處理</span><span class="sxs-lookup"><span data-stu-id="284ea-417">Buffering</span></span>
<span data-ttu-id="284ea-418">雖然有些案例很明顯適合使用批次處理，但也有許多案例可以藉由延遲處理來利用批次處理。</span><span class="sxs-lookup"><span data-stu-id="284ea-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="284ea-419">不過，延遲處理也會帶來更 hello 未預期的錯誤事件中的 hello 資料遺失的風險。</span><span class="sxs-lookup"><span data-stu-id="284ea-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="284ea-420">它是重要的 toounderstand 此風險並考慮 hello 的結果。</span><span class="sxs-lookup"><span data-stu-id="284ea-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="284ea-421">例如，請考慮追蹤 hello 巡覽記錄的每個使用者的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="284ea-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="284ea-422">每個頁面要求 hello 應用程式可以進行資料庫呼叫 toorecord hello 使用者的頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="284ea-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="284ea-423">但是，可藉由 hello 使用者的導覽活動緩衝處理，然後將此資料 toohello 資料庫傳送批次中較高的效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="284ea-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="284ea-424">您可以觸發 hello 所經過的時間和 （或） 緩衝區大小的資料庫更新。</span><span class="sxs-lookup"><span data-stu-id="284ea-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="284ea-425">例如，規則無法指定應該在 20 秒，或當 hello 緩衝區達到 1000 個項目之後處理 hello 該批次。</span><span class="sxs-lookup"><span data-stu-id="284ea-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="284ea-426">hello 下列程式碼範例使用[Reactive Extensions-Rx](https://msdn.microsoft.com/data/gg577609) tooprocess 緩衝處理的監視類別所引發的事件。</span><span class="sxs-lookup"><span data-stu-id="284ea-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="284ea-427">當 hello 緩衝區填滿或達到逾時，使用者資料的 hello 批次傳送 toohello 資料庫與資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="284ea-428">hello 下列 NavHistoryData 類別模型 hello 使用者導覽詳細資料。</span><span class="sxs-lookup"><span data-stu-id="284ea-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="284ea-429">其中包含 hello 使用者識別項等基本資訊、 hello URL 存取，而且 hello 存取時間。</span><span class="sxs-lookup"><span data-stu-id="284ea-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="284ea-430">hello NavHistoryDataMonitor 類別會負責緩衝 hello 使用者瀏覽資料 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="284ea-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="284ea-431">它包含 RecordUserNavigationEntry 方法，以引發 **OnAdded** 事件做為回應。</span><span class="sxs-lookup"><span data-stu-id="284ea-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="284ea-432">hello 下列程式碼顯示 hello 建構函式邏輯，會使用 Rx toocreate 根據 hello 事件可觀察的集合。</span><span class="sxs-lookup"><span data-stu-id="284ea-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="284ea-433">然後會使用 hello 緩衝區方法訂閱 toothis 可觀察的集合。</span><span class="sxs-lookup"><span data-stu-id="284ea-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="284ea-434">hello 多載會指定應傳送該 hello 緩衝區，每隔 20 秒或 1000 個項目。</span><span class="sxs-lookup"><span data-stu-id="284ea-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="284ea-435">hello 處理常式將所有緩衝的 hello 項目轉換成資料表值的類型，然後將該處理程序 hello 批次傳送此類型 tooa 預存程序。</span><span class="sxs-lookup"><span data-stu-id="284ea-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="284ea-436">hello 下列程式碼顯示 hello hello NavHistoryDataEventArgs 和 hello NavHistoryDataMonitor 類別的完整定義。</span><span class="sxs-lookup"><span data-stu-id="284ea-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

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

<span data-ttu-id="284ea-437">toouse 這個緩衝類別 hello 應用程式建立靜態 NavHistoryDataMonitor 物件。</span><span class="sxs-lookup"><span data-stu-id="284ea-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="284ea-438">使用者存取頁面時，每次 hello 應用程式呼叫 hello NavHistoryDataMonitor.RecordUserNavigationEntry 方法。</span><span class="sxs-lookup"><span data-stu-id="284ea-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="284ea-439">hello 緩衝邏輯繼續 tootake care of 傳送批次中的這些項目 toohello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="284ea-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="284ea-440">主要/詳細架構</span><span class="sxs-lookup"><span data-stu-id="284ea-440">Master detail</span></span>
<span data-ttu-id="284ea-441">資料表值參數適用於簡單的 INSERT 案例。</span><span class="sxs-lookup"><span data-stu-id="284ea-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="284ea-442">不過，它可以是更具挑戰性 toobatch 插入牽涉到多個資料表。</span><span class="sxs-lookup"><span data-stu-id="284ea-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="284ea-443">hello 「 主檔/明細 」 案例中是一個好範例。</span><span class="sxs-lookup"><span data-stu-id="284ea-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="284ea-444">hello 主要資料表識別 hello 主要實體。</span><span class="sxs-lookup"><span data-stu-id="284ea-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="284ea-445">一或多個明細資料表則存放有關 hello 實體的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="284ea-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="284ea-446">在此案例中，外部索引鍵關聯性會強制 hello 關聯性的詳細資料 tooa 唯一主要實體。</span><span class="sxs-lookup"><span data-stu-id="284ea-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="284ea-447">假設有一個簡化版的 PurchaseOrder 資料表及其相關聯的 OrderDetail 資料表。</span><span class="sxs-lookup"><span data-stu-id="284ea-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="284ea-448">hello 下列 TRANSACT-SQL 會建立具有四個資料行的 hello PurchaseOrder 資料表： OrderID、 OrderDate、 CustomerID 及狀態。</span><span class="sxs-lookup"><span data-stu-id="284ea-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="284ea-449">每筆訂單包含一或多個產品採購。</span><span class="sxs-lookup"><span data-stu-id="284ea-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="284ea-450">Hello PurchaseOrderDetail 資料表中擷取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="284ea-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="284ea-451">hello 下列 TRANSACT-SQL 會建立具有五個資料行的 hello PurchaseOrderDetail 資料表： OrderID、 OrderDetailID、 ProductID、 UnitPrice 和 OrderQty。</span><span class="sxs-lookup"><span data-stu-id="284ea-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="284ea-452">hello PurchaseOrderDetail 資料表中的 hello OrderID 資料行必須從 hello PurchaseOrder 資料表參考的順序。</span><span class="sxs-lookup"><span data-stu-id="284ea-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="284ea-453">hello 遵循的外部索引鍵定義強制這個限制。</span><span class="sxs-lookup"><span data-stu-id="284ea-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="284ea-454">順序 toouse 資料表值參數，您必須針對每個目標資料表的一種使用者定義資料表類型。</span><span class="sxs-lookup"><span data-stu-id="284ea-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

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

<span data-ttu-id="284ea-455">然後，定義一個可接受這幾種資料表的預存程序。</span><span class="sxs-lookup"><span data-stu-id="284ea-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="284ea-456">此程序可讓應用程式 toolocally 批次的一組訂單和訂單詳細資料的單一呼叫中。</span><span class="sxs-lookup"><span data-stu-id="284ea-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="284ea-457">hello 下列 TRANSACT-SQL 提供 hello 這個採購單範例的完整預存程序宣告。</span><span class="sxs-lookup"><span data-stu-id="284ea-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="284ea-458">在此範例中，hello 本機定義@IdentityLink資料表會儲存新插入的 hello 資料列的 hello 實際訂單編號值。</span><span class="sxs-lookup"><span data-stu-id="284ea-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="284ea-459">這些訂單識別碼會與不同 hello 暫時訂單編號的值在 hello@orders和@details資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="284ea-460">基於這個理由，hello@IdentityLink資料表再 hello OrderID 值會從連線 hello @orders toohello 真實 OrderID 的參數值 hello hello PurchaseOrder 資料表中的新資料列。</span><span class="sxs-lookup"><span data-stu-id="284ea-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="284ea-461">這個步驟之後，hello@IdentityLink資料表可促進插入 hello 訂單詳細資料，以 hello 滿足 hello foreign key 條件約束的實際 OrderID。</span><span class="sxs-lookup"><span data-stu-id="284ea-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="284ea-462">從程式碼或其他 Transact-SQL 呼叫中，都可以使用這個預存程序。</span><span class="sxs-lookup"><span data-stu-id="284ea-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="284ea-463">請參閱 hello 資料表值參數的程式碼範例的這份文件。</span><span class="sxs-lookup"><span data-stu-id="284ea-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="284ea-464">下列 TRANSACT-SQL hello 顯示 toocall hello sp_InsertOrdersBatch 的方式。</span><span class="sxs-lookup"><span data-stu-id="284ea-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

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

<span data-ttu-id="284ea-465">這個解決方案讓每個批次 toouse 一組從 1 開始的訂單編號值。</span><span class="sxs-lookup"><span data-stu-id="284ea-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="284ea-466">這些暫存 OrderID 值描述 hello hello 的批次中的關聯性，但是 hello hello 插入作業時就會判斷 hello 實際的訂單編號值。</span><span class="sxs-lookup"><span data-stu-id="284ea-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="284ea-467">您可以執行 hello 相同的陳述式 hello 前一個範例中重複，並產生唯一的訂單 hello 資料庫中。</span><span class="sxs-lookup"><span data-stu-id="284ea-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="284ea-468">因此，使用這種批次技術時，請考慮新增更多程式碼或資料庫邏輯，以防止訂單重複。</span><span class="sxs-lookup"><span data-stu-id="284ea-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="284ea-469">此範例示範即使是更複雜的資料庫作業，例如主要/詳細架構作業，也都可以透過資料表值參數進行批次處理。</span><span class="sxs-lookup"><span data-stu-id="284ea-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="284ea-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="284ea-470">UPSERT</span></span>
<span data-ttu-id="284ea-471">另一個批次處理案例涉及同時更新現有的資料列和插入新資料列。</span><span class="sxs-lookup"><span data-stu-id="284ea-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="284ea-472">這項作業有時候會參考的 tooas"UPSERT"（更新 + 插入） 作業。</span><span class="sxs-lookup"><span data-stu-id="284ea-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="284ea-473">而不是執行個別的呼叫 tooINSERT 和更新，hello MERGE 陳述式會是最適合的 toothis 工作。</span><span class="sxs-lookup"><span data-stu-id="284ea-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="284ea-474">hello MERGE 陳述式可以同時執行插入和更新作業的單一呼叫中。</span><span class="sxs-lookup"><span data-stu-id="284ea-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="284ea-475">資料表值參數可以搭配 hello MERGE 陳述式 tooperform 更新和插入。</span><span class="sxs-lookup"><span data-stu-id="284ea-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="284ea-476">例如，請考慮簡化的員工資料表，其中包含下列資料行的 hello: EmployeeID、 FirstName、 LastName、 SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="284ea-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="284ea-477">在此範例中，您可以使用該 hello SocialSecurityNumber 是唯一 tooperform 合併多名員工的 hello 事實。</span><span class="sxs-lookup"><span data-stu-id="284ea-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="284ea-478">首先，建立 hello 使用者定義資料表類型：</span><span class="sxs-lookup"><span data-stu-id="284ea-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="284ea-479">接下來，建立預存程序，或撰寫程式碼會使用 hello MERGE 陳述式 tooperform hello 更新和插入。</span><span class="sxs-lookup"><span data-stu-id="284ea-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="284ea-480">hello 下列範例會使用 hello MERGE 陳述式資料表值參數， @employees，EmployeeTableType 型別。</span><span class="sxs-lookup"><span data-stu-id="284ea-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="284ea-481">hello 的 hello 內容@employees此處未顯示資料表。</span><span class="sxs-lookup"><span data-stu-id="284ea-481">hello contents of hello @employees table are not shown here.</span></span>

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

<span data-ttu-id="284ea-482">如需詳細資訊，請參閱 hello 文件集和 hello MERGE 陳述式的範例。</span><span class="sxs-lookup"><span data-stu-id="284ea-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="284ea-483">相同的工作無法執行多個步驟中的 hello 預存程序呼叫，以個別的 INSERT 和 UPDATE 作業，雖然 hello MERGE 陳述式會更有效率。</span><span class="sxs-lookup"><span data-stu-id="284ea-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="284ea-484">資料庫程式碼也可以建構 TRANSACT-SQL 呼叫使用直接而不需要針對插入和更新的兩個資料庫呼叫 hello MERGE 陳述式。</span><span class="sxs-lookup"><span data-stu-id="284ea-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="284ea-485">建議摘要</span><span class="sxs-lookup"><span data-stu-id="284ea-485">Recommendation summary</span></span>
<span data-ttu-id="284ea-486">hello 下列清單提供 hello 批次處理本主題所討論的建議的摘要：</span><span class="sxs-lookup"><span data-stu-id="284ea-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="284ea-487">使用緩衝和批次處理 tooincrease hello 效能和延展性的 SQL Database 應用程式。</span><span class="sxs-lookup"><span data-stu-id="284ea-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="284ea-488">了解批次處理/緩衝處理與復原之間的權衡取捨完全 hello。</span><span class="sxs-lookup"><span data-stu-id="284ea-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="284ea-489">在角色失敗時，遺失的業務關鍵資料的未處理的批次的 hello 風險程度可能會超過 hello 批次作業的效能優勢。</span><span class="sxs-lookup"><span data-stu-id="284ea-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="284ea-490">嘗試 tookeep 所有呼叫 toohello 資料庫內的單一資料中心 tooreduce 延遲。</span><span class="sxs-lookup"><span data-stu-id="284ea-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="284ea-491">如果您選擇單一批次處理技術，資料表值參數提供 hello 最佳效能和彈性。</span><span class="sxs-lookup"><span data-stu-id="284ea-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="284ea-492">最快的 hello 插入效能，請遵循這些一般指導方針，但測試您的案例：</span><span class="sxs-lookup"><span data-stu-id="284ea-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="284ea-493">如果 < 100 個資料列，使用單一參數化 INSERT 命令。</span><span class="sxs-lookup"><span data-stu-id="284ea-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="284ea-494">如果 < 1000 個資料列，使用資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="284ea-495">如果 >= 1000 個資料列，使用 SqlBulkCopy。</span><span class="sxs-lookup"><span data-stu-id="284ea-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="284ea-496">針對更新和刪除作業，判斷 hello hello 資料表參數中的每個資料列上的正確作業的預存程序邏輯中使用資料表值參數。</span><span class="sxs-lookup"><span data-stu-id="284ea-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="284ea-497">批次大小的指導方針：</span><span class="sxs-lookup"><span data-stu-id="284ea-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="284ea-498">使用 hello 最大批次大小對您的應用程式和商務需求的有意義。</span><span class="sxs-lookup"><span data-stu-id="284ea-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="284ea-499">平衡 hello 效能提升的大型批次 hello 的暫時性或災難性失敗的風險。</span><span class="sxs-lookup"><span data-stu-id="284ea-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="284ea-500">重試次數的 hello 結果或 hello hello 批次中的資料遺失是什麼？</span><span class="sxs-lookup"><span data-stu-id="284ea-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="284ea-501">測試 hello 最大批次大小 tooverify，SQL Database 不會拒絕它。</span><span class="sxs-lookup"><span data-stu-id="284ea-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="284ea-502">建立控制批次處理，例如 hello 批次大小或緩衝時間間隔 hello 組態設定。</span><span class="sxs-lookup"><span data-stu-id="284ea-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="284ea-503">這些設定提供彈性。</span><span class="sxs-lookup"><span data-stu-id="284ea-503">These settings provide flexibility.</span></span> <span data-ttu-id="284ea-504">您可以變更批次處理行為在生產環境中的，而不必重新部署 hello 雲端服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="284ea-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="284ea-505">避免在一個資料庫的單一資料表上平行執行批次。</span><span class="sxs-lookup"><span data-stu-id="284ea-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="284ea-506">如果您選擇 toodivide 單一批次多個背景工作執行緒上，執行測試 toodetermine hello 理想的執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="284ea-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="284ea-507">超過未確定的臨界值之後，更多的執行緒只會降低效能，不會提高效能。</span><span class="sxs-lookup"><span data-stu-id="284ea-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="284ea-508">在更多案例下，考慮依大小和時間緩衝來實作批次處理。</span><span class="sxs-lookup"><span data-stu-id="284ea-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="284ea-509">後續步驟</span><span class="sxs-lookup"><span data-stu-id="284ea-509">Next steps</span></span>
<span data-ttu-id="284ea-510">本文著重於資料庫設計和編碼技術相關 toobatching 可以改善您的應用程式效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="284ea-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="284ea-511">但這只是整體策略中的一個因素。</span><span class="sxs-lookup"><span data-stu-id="284ea-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="284ea-512">如需詳細的方式 tooimprove 效能和延展性，請參閱[單一資料庫的 Azure SQL Database 效能指引](sql-database-performance-guidance.md)和[彈性集區的價格和效能考量](sql-database-elastic-pool-guidance.md)。</span><span class="sxs-lookup"><span data-stu-id="284ea-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

