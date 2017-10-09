---
title: "aaaUsing 彈性資料庫用戶端程式庫 Dapper |Microsoft 文件"
description: "搭配使用彈性資料庫用戶端程式庫與 Dapper。"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>搭配使用彈性資料庫用戶端程式庫與 Dapper
這份文件適用於不依賴 Dapper toobuild 應用程式，但也會想 tooembrace[彈性資料庫工具](sql-database-elastic-scale-introduction.md)toocreate 的實作分區化 tooscale 出其資料層應用程式。  本文件說明的彈性資料庫工具的必要 toointegrate Dapper 架構應用程式中的 hello 變更。 我們將焦點在編寫 hello 彈性資料庫分區管理和資料依存路由與 Dapper。 

**範例程式碼**： [Azure SQL Database - Dapper 整合的彈性資料庫工具](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f)。

整合**Dapper**和**DapperExtensions** hello 與 Azure SQL Database 的彈性資料庫用戶端程式庫很容易。 您的應用程式可以使用資料依存路由，方法是變更 hello 建立和開啟新[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)物件 toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 從呼叫[用戶端程式庫](http://msdn.microsoft.com/library/azure/dn765902.aspx)。 這會限制您的應用程式 tooonly 其中建立並開啟新的連接中的變更。 

## <a name="dapper-overview"></a>Dapper 概觀
**Dapper** 是物件關聯式對應程式。 它對應來自您應用程式 tooa 關聯式資料庫 （反之亦然） 的.NET 物件。 hello 的 hello 範例程式碼的第一個部分說明您可以將 hello 彈性資料庫用戶端程式庫整合與 Dapper 為基礎的應用程式的方式。 hello 的 hello 範例程式碼的第二個部分將說明如何使用 Dapper 和 DapperExtensions 時 toointegrate。  

Dapper hello 對應工具功能會提供擴充方法，簡化執行或查詢 hello 資料庫正在提交 T-SQL 陳述式的資料庫連線。 比方說，Dapper 可讓您的.NET 物件與 hello 參數的 SQL 陳述式之間的簡單 toomap **Execute**呼叫或 tooconsume hello 您的 SQL 查詢結果為.NET 物件使用**查詢**Dapper 的呼叫。 

使用 DapperExtensions，當您不再需要 tooprovide hello SQL 陳述式。 擴充方法，例如**GetList**或**插入**hello 資料庫連線建立 hello hello 幕後的 SQL 陳述式。

Dapper 以及 DapperExtensions 的另一個優點是 hello 應用程式控制項 hello 建立 hello 資料庫連接。 這有助於互動 hello 彈性資料庫用戶端程式庫的 broker 資料庫為基礎的 shardlet toodatabases hello 對應的連接。

tooget hello Dapper 組件，請參閱[Dapper 點 net](http://www.nuget.org/packages/Dapper/)。 針對 hello Dapper 擴充功能，請參閱[DapperExtensions](http://www.nuget.org/packages/DapperExtensions)。

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>快速查看 hello 彈性資料庫用戶端程式庫
與 hello 彈性資料庫用戶端程式庫，您會定義呼叫的應用程式資料的資料分割*shardlet* 、 將它們對應 toodatabases，和它們所識別*分區化索引鍵*。 您可以擁有所需數量的資料庫，並將 Shardlet 分散於這些資料庫。 hello 對應的分區化索引鍵值 toohello 資料庫儲存 hello 程式庫的應用程式開發介面所提供的分區對應。 這項功能稱為 **分區對應管理**。 hello 分區對應也可做為 hello broker 的要求進行分區化索引鍵的資料庫連線。 這項功能會參考的 tooas**資料依存路由**。

![分區對應和資料相依路由][1]

hello 分區對應管理員防止不一致的檢視為 shardlet 資料 hello 資料庫上發生並行的 shardlet 管理作業時可能發生的使用者。 toodo，hello 分區對應 broker hello 資料庫連接，以便與 hello 程式庫所建置的應用程式。 當分區管理作業可能會影響 hello shardlet 時，這樣 hello 分區對應功能 tooautomatically 終止資料庫連接。 

而不是使用 Dapper hello 傳統方式 toocreate 連接，我們需要 toouse hello [OpenConnectionForKey 方法](http://msdn.microsoft.com/library/azure/dn824099.aspx)。 這樣可以確保所有 hello 驗證都進行連接都管理正確分區之間的任何資料移動時。

### <a name="requirements-for-dapper-integration"></a>Dapper 整合需求
當使用 hello 彈性資料庫用戶端程式庫和 hello Dapper 應用程式開發介面，我們想要 tooretain hello 下列屬性：

* **向外延展**： 我們想 tooadd 或 hello 資料 hello 分區化應用程式層的視 hello 容量需求的 hello 應用程式中移除資料庫。 
* **一致性**： 由於我們的應用程式會向外延展使用分區化中，我們需要 tooperform 資料依存路由。 因此，我們想 toouse hello 資料依存路由功能 hello 文件庫 toodo。 特別是，我們想 tooretain hello 驗證，而且透過順序 tooavoid 損毀或不正確的查詢結果中的 hello 分區對應管理員代理的連接所提供的一致性保證。 這可確保該給定 shardlet 的連線 tooa 拒絕或停止時 （例如） hello shardlet 目前移動的 tooa 不同分區使用分割/合併 Api。
* **物件對應**： 我們想要 tooretain hello 的方便性，不論 hello Dapper tootranslate hello 應用程式中的類別和基礎資料庫結構的 hello 之間所提供的對應。 

hello 下節提供這些需求為基礎的應用程式的指引**Dapper**和**DapperExtensions**。

## <a name="technical-guidance"></a>技術指導
### <a name="data-dependent-routing-with-dapper"></a>Dapper 的資料相依路由
Dapper，與 hello 應用程式是通常負責建立及開啟 hello 連線 toohello 基礎資料庫。 Hello 應用程式所指定型別 T，Dapper 傳回查詢結果的型別 T Dapper.NET 集合執行 hello 對應從 hello T-SQL 結果資料列 toohello 物件為類型 t。同樣地，Dapper 將.NET 物件對應至 SQL 值或資料操作語言 (DML) 陳述式的參數。 Dapper 提供這項功能透過 hello 規則的擴充方法[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello ADO.NET SQL 用戶端程式庫中的物件。 hello hello Elastic Scale Api 所傳回的 DDR 的 SQL 連接也會定期[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)物件。 這可讓我們 toodirectly 使用 Dapper 延伸 hello hello 用戶端程式庫的 DDR API，所傳回的類型，所以也是簡單的 SQL 用戶端連接。

這些觀察後讓直接 toouse 連線的 Dapper 代理 hello 彈性資料庫用戶端程式庫。

（從 hello 隨附的範例) 這個程式碼範例將示範 hello 方法其中 hello 分區化索引鍵由 hello 應用程式 toohello 文件庫 toobroker hello 連接 toohello 正確分區。   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

hello 呼叫 toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API 取代 hello 預設建立及開啟 SQL 用戶端連接。 hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)呼叫採用所需的資料依存路由 hello 引數： 

* hello 分區對應 tooaccess hello 資料依存路由介面
* hello 分區化索引鍵 tooidentify hello shardlet
* hello 認證 （使用者名稱和密碼） tooconnect toohello 分區

hello 分區對應物件會建立保留 hello 指定分區化索引鍵的 hello shardlet 連線 toohello 分區。 hello 彈性資料庫用戶端應用程式開發介面也標記 hello 連接 tooimplement 其一致性保證。 因為 hello 呼叫太[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)傳回規則的 SQL 用戶端連線物件、 hello 後續呼叫 toohello **Execute**從 Dapper 如下所示的擴充方法 hello 標準 Dapper練習。

查詢工作非常 hello 相同方式-您第一次開啟 hello 連線使用[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)從 hello 用戶端應用程式開發介面。 然後您可以使用 hello 一般 Dapper 擴充功能方法 toomap hello SQL 查詢結果為.NET 物件：

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

請注意該 hello**使用**與 hello DDR 連接範圍會封鎖 hello 區塊 toohello 一個分區處於 tenantId1 內的所有資料庫作業。 hello 查詢只會傳回儲存在 hello 目前分區，但是 hello 儲存在任何其他分區上的項目上的部落格。 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Dapper 和 DapperExtensions 的資料相依路由
Dapper 隨附的其他擴充功能時，可以提供進一步的方便以及抽象從 hello 資料庫開發資料庫應用程式的生態系統。 DapperExtensions 就是一個範例。 

在您的應用程式中使用 DapperExtensions，不會改變建立和管理資料庫連線的方式。 它仍然是 hello 應用程式的責任 tooopen 連線，以及一般的 SQL 用戶端連線物件會預期收到 hello 擴充方法。 我們可以依賴 hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx)如上面所述。 Hello 為下列程式碼範例會顯示 hello 唯一的變更是，我們不會再有 toowrite hello T-SQL 陳述式：

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

此外，這裡有 hello hello 查詢的程式碼範例： 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>處理暫時性錯誤
hello Microsoft Patterns & Practices 團隊發行的 hello[暫時性錯誤處理應用程式區塊](http://msdn.microsoft.com/library/hh680934.aspx)toohelp 應用程式開發人員降低 hello 雲端中執行時所遇到的常見暫時性錯誤狀況。 如需詳細資訊，請參閱[堅持不懈、 所有勝利密碼： 使用暫時性錯誤處理應用程式區塊 hello](http://msdn.microsoft.com/library/dn440719.aspx)。

hello 程式碼範例會依賴 hello 暫時性錯誤文件庫 tooprotect 針對暫時性錯誤。 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** hello 在上述程式碼會定義為**SqlDatabaseTransientErrorDetectionStrategy** 10，和 5 秒的重試計數等候重試之間的時間。 如果您正在使用交易，請確定您重試的範圍會回到 toohello 之暫時性錯誤的 hello 案例中的 hello 交易的開頭。

## <a name="limitations"></a>限制
這份文件中所述的 hello 方法需要有幾項限制：

* 本文件的 hello 範例程式碼不會示範如何跨分區 toomanage 結構描述。
* 指定要求，我們假設其所有資料庫處理都包含在單一分區中的 hello hello 要求所提供的分區化索引鍵識別。 不過，這項假設不一定包含，比方說，不可能 toomake 分區化索引鍵可用時。 tooaddress，hello 彈性資料庫用戶端程式庫包含 hello [MultiShardQuery 類別](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx)。 hello 類別會實作抽象的查詢數個分區的連線。 使用搭配 Dapper MultiShardQuery 已超出本文件 hello 範圍。

## <a name="conclusion"></a>結論
使用 Dapper 與 DapperExtensions 的應用程式可以輕易地受益於 Azure SQL Database 的彈性資料庫工具。 Hello 這份文件中所述的步驟，透過這些應用程式可用於 hello 工具的功能資料依存路由，方法是變更 hello 建立和開啟新[SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)物件 toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello 彈性資料庫用戶端程式庫的呼叫。 這會限制 hello 應用程式的變更需要的 toothose 數位其中建立並開啟新的連接。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
