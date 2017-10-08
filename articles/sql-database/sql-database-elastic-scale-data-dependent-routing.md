---
title: "相依路由與 Azure SQL Database aaaData |Microsoft 文件"
description: "如何 toouse hello ShardMapManager 資料依存路由，在 Azure SQL Database 分區化資料庫的一項功能的.NET 應用程式中的類別"
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
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>資料相依路由
**資料依存路由**hello 能力 toouse hello 資料查詢 tooroute hello 要求 tooan 適當資料庫中。 這是使用分區化資料庫時的一種基本模式。 hello 要求內容也可能使用的 tooroute hello 要求，特別是當 hello 分區化索引鍵不是 hello 查詢的一部分。 每個特定的查詢或交易中使用資料依存路由的應用程式是受限制的 tooaccessing 單一資料庫，每個要求。 Hello Azure SQL Database 彈性的工具，在以 hello 完成此路由 **[ShardMapManager 類別](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)** ADO.NET 應用程式中。

hello 應用程式不需要 tootrack，不同的連接字串或不同的配量的 hello 分區化環境中的資料與相關聯的 DB 位置。 相反地，hello[分區對應管理員](sql-database-elastic-scale-shard-map-management.md)開啟連線 toohello 正確的資料庫需要時，根據 hello 分區對應和 hello 的 hello hello 應用程式要求目標的 hello 分區化索引鍵的值中的 hello 資料。 hello 索引鍵通常是 hello *customer_id*， *tenant_id*， *date_key*，或某些其他特定識別碼 hello 資料庫要求的基本參數)。 

如需詳細資訊，請參閱 [Scaling Out SQL Server with Data Dependent Routing (使用資料相依路由相應放大 SQL Server)](https://technet.microsoft.com/library/cc966448.aspx)。

## <a name="download-hello-client-library"></a>下載 hello 用戶端程式庫
tooget hello 類別安裝 hello[彈性資料庫用戶端程式庫](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/)。 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>在資料相依路由應用程式中使用 ShardMapManager
應用程式應該具現化 hello **ShardMapManager**在初始化期間，使用 hello factory 呼叫 **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**。 此範例中會初始化 **ShardMapManager** 及其包含的特定 **ShardMap**。 此範例中會顯示 hello GetSqlShardMapManager 和[GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx)方法。

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>使用最低權限認證可能讓 hello 分區對應
如果應用程式不操作 hello 分區對應本身，hello hello factory 方法中使用的認證上至少應有只唯讀權限 hello**全域分區對應**資料庫。 這些認證所用認證 tooopen 連線 toohello 分區對應管理員通常不同。 另請參閱[使用 tooaccess hello 彈性資料庫用戶端程式庫的認證](sql-database-elastic-scale-manage-credentials.md)。 

## <a name="call-hello-openconnectionforkey-method"></a>呼叫 hello OpenConnectionForKey 方法
hello  **[ShardMap.OpenConnectionForKey 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**傳回準備好發行的 hello hello 值為基礎的命令 toohello 適當資料庫的 ADO.Net 連接**金鑰**參數。 分區資訊快取 hello 應用程式中的 hello **ShardMapManager**，因此這些要求通常不包含針對 hello 資料庫尋查**全域分區對應**資料庫。 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* hello**金鑰**參數作為查閱索引鍵到 hello 分區對應 toodetermine hello 適當資料庫 hello 要求。 
* hello **connectionString**是使用的 toopass hello 想要連接的唯一 hello 使用者認證。 沒有資料庫名稱或伺服器名稱包含在此*connectionString*因為 hello 方法會判斷 hello 資料庫和伺服器 hello **ShardMap**。 
* hello  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)** 應該設定太**ConnectionOptions.Validate**如果分區對應所在的環境可能會變更，且資料列可能會移動 tooother 資料庫分割或合併作業的結果。 這項作業包括簡短查詢 toohello 本機分區對應 hello 連線前的 hello 目標資料庫 （不 toohello 全域分區對應） 會傳遞 toohello 應用程式。 

Hello 分區對應管理員 hello hello 本機分區對應的驗證，就會失敗 （表示 hello 快取不正確），如果將查詢 hello 全域分區對應 tooobtain hello 新正確值 hello 查閱而言，更新 hello 快取，以及取得並傳回 hello適當的資料庫連接。 

唯有當應用程式在線上，分區對應的變更是非預期之時，才使用 **ConnectionOptions.None** 。 在此情況下，快取的 hello 值可以假設 tooalways 正確，以及可以放心地略過 hello 額外反覆存取驗證呼叫 toohello 目標資料庫。 這會減少資料庫流量。 hello **connectionOptions**可能也透過組態檔 tooindicate 中的值是否應該分區化變更或設定不會在一段時間。  

這個範例會使用整數索引鍵的 hello 值**CustomerID**，並使用**ShardMap**名為物件**customerShardMap**。  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
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

hello **OpenConnectionForKey**方法會傳回新的連接已經開啟 toohello 正確資料庫。 以這種方式使用連接仍可充分利用 ADO.Net 連接共用。 只要交易和要求都可藉由一個分區一次，這應該是 hello 只有修改需要已經使用 ADO.Net 應用程式中。 

hello  **[OpenConnectionForKeyAsync 方法](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**也會提供，若您的應用程式會使用非同步程式設計與 ADO.Net。 其行為是 hello 資料依存路由 ADO 的對等。網路的 **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)** 方法。

## <a name="integrating-with-transient-fault-handling"></a>與暫時性錯誤處理整合
開發 hello 雲端中的資料存取應用程式中的最佳做法是的 tooensure 暫時性失敗所捕捉 hello 應用程式，而且 hello 作業會擲回錯誤之前項目重試數次。 [暫時性錯誤處理](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx)中討論雲端應用程式的暫時性錯誤處理。 

暫時性錯誤處理可以同時存在自然 hello 資料依存路由的模式。 hello 關鍵需求是 tooretry hello 整個資料存取的要求包括 hello**使用**取得 hello 資料依存路由連接的區塊。 上述的 hello 範例可以改寫如下 （請注意反白顯示的變更）。 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>範例 - 資料相依路由與暫時性錯誤處理
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
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


封裝需要 tooimplement 暫時性錯誤處理會自動下載當您建置 hello 彈性資料庫範例應用程式。 另外也可以從 [企業程式庫 - 暫時性錯誤處理應用程式區塊](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)(英文) 取得封裝。 請使用 6.0 版或更新版本。 

## <a name="transactional-consistency"></a>交易一致性
所有作業本機 tooa 分區都保證交易的內容。 例如，透過資料依存路由送出的交易執行 hello 目標分區 hello 連線 hello 範圍內。 目前無法將多個連接編列到交易中，因此對於跨分區執行的作業，不提供交易式保證。

## <a name="next-steps"></a>後續步驟
toodetach 分區或 tooreattach 分區，請參閱[使用 hello RecoveryManager 類別 toofix 分區對應問題](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

