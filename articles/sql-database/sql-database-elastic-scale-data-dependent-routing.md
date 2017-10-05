---
title: "與 Azure SQL Database 的資料相依路由 | Microsoft Docs"
description: "如何在 .NET 應用程式中將 ShardMapManager 類別用於資料相依路由 (Azure SQL Database 中的分區化資料庫的一項功能)"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 6b68bbb0133afd1493acdb58f79f3eeaf6a8d7cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="data-dependent-routing"></a><span data-ttu-id="d7bb8-103">資料相依路由</span><span class="sxs-lookup"><span data-stu-id="d7bb8-103">Data dependent routing</span></span>
<span data-ttu-id="d7bb8-104">**資料相依路由** 是可使用查詢中的資料，將要求路由至適當的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-104">**Data dependent routing** is the ability to use the data in a query to route the request to an appropriate database.</span></span> <span data-ttu-id="d7bb8-105">這是使用分區化資料庫時的一種基本模式。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-105">This is a fundamental pattern when working with sharded databases.</span></span> <span data-ttu-id="d7bb8-106">要求內容也可能會用於路由要求，特別是如果分區化索引鍵不是查詢的一部分。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-106">The request context may also be used to route the request, especially if the sharding key is not part of the query.</span></span> <span data-ttu-id="d7bb8-107">在使用資料相依路由的應用程式中，每個特定的查詢或交易會限制每個要求只能存取單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-107">Each specific query or transaction in an application using data dependent routing is restricted to accessing a single database per request.</span></span> <span data-ttu-id="d7bb8-108">針對 Azure SQL Database Elastic 工具，此路由會在 ADO.NET 應用程式中使用 **[ShardMapManager 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**來完成。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-108">For the Azure SQL Database Elastic tools, this routing is accomplished with the **[ShardMapManager class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** in ADO.NET applications.</span></span>

<span data-ttu-id="d7bb8-109">應用程式不需要在分區化環境中追蹤不同的連接字串或與不同資料片段相關聯的 DB 位置。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-109">The application does not need to track various connection strings or DB locations associated with different slices of data in the sharded environment.</span></span> <span data-ttu-id="d7bb8-110">相反地， [分區對應管理員](sql-database-elastic-scale-shard-map-management.md) 會根據分區對應中的資料和分區化索引鍵的值 (應用程式要求的目標)，在必要時開啟正確資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-110">Instead, the [Shard Map Manager](sql-database-elastic-scale-shard-map-management.md) opens connections to the correct databases when needed, based on the data in the shard map and the value of the sharding key that is the target of the application’s request.</span></span> <span data-ttu-id="d7bb8-111">此索引鍵通常是 customer_id、tenant_id、date_key，或作為資料庫要求基本參數的其他一些特定的識別項)。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-111">The key is typically the *customer_id*, *tenant_id*, *date_key*, or some other specific identifier that is a fundamental parameter of the database request).</span></span> 

<span data-ttu-id="d7bb8-112">如需詳細資訊，請參閱 [Scaling Out SQL Server with Data Dependent Routing (使用資料相依路由相應放大 SQL Server)](https://technet.microsoft.com/library/cc966448.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-112">For more information, see [Scaling Out SQL Server with Data Dependent Routing](https://technet.microsoft.com/library/cc966448.aspx).</span></span>

## <a name="download-the-client-library"></a><span data-ttu-id="d7bb8-113">下載用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="d7bb8-113">Download the client library</span></span>
<span data-ttu-id="d7bb8-114">若要取得類別，請安裝 [彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-114">To get the class, install the [Elastic Database Client Library](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/).</span></span> 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a><span data-ttu-id="d7bb8-115">在資料相依路由應用程式中使用 ShardMapManager</span><span class="sxs-lookup"><span data-stu-id="d7bb8-115">Using a ShardMapManager in a data dependent routing application</span></span>
<span data-ttu-id="d7bb8-116">應用程式應該在初始化期間，使用 Factory 呼叫 **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)** 來具現化 **ShardMapManager**。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-116">Applications should instantiate the **ShardMapManager** during initialization, using the factory call **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**.</span></span> <span data-ttu-id="d7bb8-117">此範例中會初始化 **ShardMapManager** 及其包含的特定 **ShardMap**。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-117">In this example, both a **ShardMapManager** and a specific **ShardMap** that it contains are initialized.</span></span> <span data-ttu-id="d7bb8-118">這個範例示範 GetSqlShardMapManager 和 [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) 方法。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-118">This example shows the GetSqlShardMapManager and [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) methods.</span></span>

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-the-shard-map"></a><span data-ttu-id="d7bb8-119">盡可能使用最低權限的認證來取得分區對應</span><span class="sxs-lookup"><span data-stu-id="d7bb8-119">Use lowest privilege credentials possible for getting the shard map</span></span>
<span data-ttu-id="d7bb8-120">如果應用程式不會自行操作分區對應，用於 Factory 方法中的認證在 **全域分區對應** 資料庫上應該只有唯讀權限。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-120">If an application is not manipulating the shard map itself, the credentials used in the factory method should have just read-only permissions on the **Global Shard Map** database.</span></span> <span data-ttu-id="d7bb8-121">這些認證通常不同於用來對分區對應管理員開啟連接的認證。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-121">These credentials are typically different from credentials used to open connections to the shard map manager.</span></span> <span data-ttu-id="d7bb8-122">另請參閱 [用來存取彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-122">See also [Credentials used to access the Elastic Database client library](sql-database-elastic-scale-manage-credentials.md).</span></span> 

## <a name="call-the-openconnectionforkey-method"></a><span data-ttu-id="d7bb8-123">呼叫 OpenConnectionForKey 方法</span><span class="sxs-lookup"><span data-stu-id="d7bb8-123">Call the OpenConnectionForKey method</span></span>
<span data-ttu-id="d7bb8-124">**[ShardMap.OpenConnectionForKey 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** 傳回的 ADO.Net 連接可根據 **key** 參數的值，對適當的資料庫發出命令。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-124">The **[ShardMap.OpenConnectionForKey method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)** returns an ADO.Net connection ready for issuing commands to the appropriate database based on the value of the **key** parameter.</span></span> <span data-ttu-id="d7bb8-125">**ShardMapManager** 會將分區資訊快取在應用程式中，因此這些要求通常不需要針對**全域分區對應**資料庫進行資料庫尋查。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-125">Shard information is cached in the application by the **ShardMapManager**, so these requests do not typically involve a database lookup against the **Global Shard Map** database.</span></span> 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* <span data-ttu-id="d7bb8-126">**key** 參數做為分區對應中的查閱索引鍵，以決定要求的適當資料庫。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-126">The **key** parameter is used as a lookup key into the shard map to determine the appropriate database for the request.</span></span> 
* <span data-ttu-id="d7bb8-127">**connectionString** 只用來傳遞使用者認證給所需的連接。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-127">The **connectionString** is used to pass only the user credentials for the desired connection.</span></span> <span data-ttu-id="d7bb8-128">此 *connectionString* 中不含任何資料庫名稱或伺服器名稱，因為此方法會使用 **ShardMap**來決定資料庫和伺服器。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-128">No database name or server name are included in this *connectionString* since the method will determine the database and server using the **ShardMap**.</span></span> 
* <span data-ttu-id="d7bb8-129">若分區對應所在的環境可能變更，且資料列可能會移動到其他的資料庫成為分割或合併作業的結果，則 **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** 應設為 **ConnectionOptions.Validate**。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-129">The **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** should be set to **ConnectionOptions.Validate** if an environment where shard maps may change and rows may move to other databases as a result of split or merge operations.</span></span> <span data-ttu-id="d7bb8-130">這牽涉到在將連接傳遞至應用程式之前，對目標資料庫上的本機分區對應 (不是全域分區對應) 的簡短查詢。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-130">This involves a brief query to the local shard map on the target database (not to the global shard map) before the connection is delivered to the application.</span></span> 

<span data-ttu-id="d7bb8-131">如果本機分區對應驗證失敗 (表示快取不正確)，分區對應管理員會查詢全域分區對應來取得查閱的新正確值、更新快取，然後取得並傳回適當的資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-131">If the validation against the local shard map fails (indicating that the cache is incorrect), the Shard Map Manager will query the global shard map to obtain the new correct value for the lookup, update the cache, and obtain and return the appropriate database connection.</span></span> 

<span data-ttu-id="d7bb8-132">唯有當應用程式在線上，分區對應的變更是非預期之時，才使用 **ConnectionOptions.None** 。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-132">Use **ConnectionOptions.None** only when shard mapping changes are not expected while an application is online.</span></span> <span data-ttu-id="d7bb8-133">在此情況下，快取的值可假定為永遠正確，可放心地略過對於目標資料庫的額外往返驗證呼叫。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-133">In that case, the cached values can be assumed to always be correct, and the extra round-trip validation call to the target database can be safely skipped.</span></span> <span data-ttu-id="d7bb8-134">這會減少資料庫流量。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-134">That reduces database traffic.</span></span> <span data-ttu-id="d7bb8-135">也可透過組態檔中的值來設定 **connectionOptions** ，以指出在一段時間內是否預期有分區化變更。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-135">The **connectionOptions** may also be set via a value in a configuration file to indicate whether sharding changes are expected or not during a period of time.</span></span>  

<span data-ttu-id="d7bb8-136">此範例會利用名為 **customerShardMap** 的 **ShardMap** 物件，使用整數索引鍵值 **CustomerID**。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-136">This example uses the value of an integer key **CustomerID**, using a **ShardMap** object named **customerShardMap**.</span></span>  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect to the shard for that customer ID. No need to call a SqlConnection 
    // constructor followed by the Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

<span data-ttu-id="d7bb8-137">**OpenConnectionForKey** 方法會傳回新的已開啟連接至正確的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-137">The **OpenConnectionForKey** method returns a new already-open connection to the correct database.</span></span> <span data-ttu-id="d7bb8-138">以這種方式使用連接仍可充分利用 ADO.Net 連接共用。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-138">Connections utilized in this way still take full advantage of ADO.Net connection pooling.</span></span> <span data-ttu-id="d7bb8-139">只要一次一個分區就可滿足交易和要求，則已經使用 ADO.Net 的應用程式中只需要如此修改。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-139">As long as transactions and requests can be satisfied by one shard at a time, this should be the only modification necessary in an application already using ADO.Net.</span></span> 

<span data-ttu-id="d7bb8-140">如果您的應用程式將非同步程式設計與 ADO.Net 搭配使用，則也可以使用 **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-140">The **[OpenConnectionForKeyAsync method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)** is also available if your application makes use asynchronous programming with ADO.Net.</span></span> <span data-ttu-id="d7bb8-141">其行為相當於 ADO.Net **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** 方法的資料相依路由。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-141">Its behavior is the data dependent routing equivalent of ADO.Net's **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** method.</span></span>

## <a name="integrating-with-transient-fault-handling"></a><span data-ttu-id="d7bb8-142">與暫時性錯誤處理整合</span><span class="sxs-lookup"><span data-stu-id="d7bb8-142">Integrating with transient fault handling</span></span>
<span data-ttu-id="d7bb8-143">在雲端中開發資料存取應用程式時，最佳做法就是確保應用程式會攔截暫時性錯誤，並且將作業重試數次之後才會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-143">A best practice in developing data access applications in the cloud is to ensure that transient faults are caught by the app, and that the operations are retried several times before throwing an error.</span></span> <span data-ttu-id="d7bb8-144">[暫時性錯誤處理](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx)中討論雲端應用程式的暫時性錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-144">Transient fault handling for cloud applications is discussed at [Transient Fault Handling](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx).</span></span> 

<span data-ttu-id="d7bb8-145">暫時性錯誤處理可以自然地與資料相依路由模式並存。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-145">Transient fault handling can coexist naturally with the Data Dependent Routing pattern.</span></span> <span data-ttu-id="d7bb8-146">主要需求是重試整個資料存取要求，包括用以取得資料相依路由連接的 **using** 區塊。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-146">The key requirement is to retry the entire data access request including the **using** block that obtained the data-dependent routing connection.</span></span> <span data-ttu-id="d7bb8-147">上述範例可以改寫如下 (請注意反白顯示的變更)。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-147">The example above could be rewritten as follows (note highlighted change).</span></span> 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a><span data-ttu-id="d7bb8-148">範例 - 資料相依路由與暫時性錯誤處理</span><span class="sxs-lookup"><span data-stu-id="d7bb8-148">Example - data dependent routing with transient fault handling</span></span>
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect to the shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


<span data-ttu-id="d7bb8-149">當您建置彈性資料庫範例應用程式時，自動會下載實作暫時性錯誤處理所需的封裝。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-149">Packages necessary to implement transient fault handling are downloaded automatically when you build the elastic database sample application.</span></span> <span data-ttu-id="d7bb8-150">另外也可以從 [企業程式庫 - 暫時性錯誤處理應用程式區塊](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)(英文) 取得封裝。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-150">Packages are also available separately at [Enterprise Library - Transient Fault Handling Application Block](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/).</span></span> <span data-ttu-id="d7bb8-151">請使用 6.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-151">Use version 6.0 or later.</span></span> 

## <a name="transactional-consistency"></a><span data-ttu-id="d7bb8-152">交易一致性</span><span class="sxs-lookup"><span data-stu-id="d7bb8-152">Transactional consistency</span></span>
<span data-ttu-id="d7bb8-153">對於分區範圍內的所有作業，都保證交易式屬性。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-153">Transactional properties are guaranteed for all operations local to a shard.</span></span> <span data-ttu-id="d7bb8-154">例如，透過資料相依路由提交的交易，都在連接的目標分區範圍內執行。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-154">For example, transactions submitted through data-dependent routing execute within the scope of the target shard for the connection.</span></span> <span data-ttu-id="d7bb8-155">目前無法將多個連接編列到交易中，因此對於跨分區執行的作業，不提供交易式保證。</span><span class="sxs-lookup"><span data-stu-id="d7bb8-155">At this time, there are no capabilities provided for enlisting multiple connections into a transaction, and therefore there are no transactional guarantees for operations performed across shards.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7bb8-156">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d7bb8-156">Next steps</span></span>
<span data-ttu-id="d7bb8-157">若要中斷連結分區或重新附加分區，請參閱 [使用 RecoveryManager 類別來修正分區對應問題](sql-database-elastic-database-recovery-manager.md)</span><span class="sxs-lookup"><span data-stu-id="d7bb8-157">To detach a shard, or to reattach a shard, see [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md)</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

