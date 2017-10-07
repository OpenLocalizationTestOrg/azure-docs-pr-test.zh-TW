---
title: "使用 Entity Framework aaaUsing 彈性資料庫用戶端程式庫 |Microsoft 文件"
description: "使用彈性資料庫用戶端程式庫與和 Entity Framework 來編寫資料庫"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>搭配使用彈性資料庫用戶端程式庫與 Entity Framework
這份文件的 Entity Framework 應用程式，都需要以 hello toointegrate 顯示 hello 變更[彈性資料庫工具](sql-database-elastic-scale-introduction.md)。 hello 重點在於撰寫[分區對應管理](sql-database-elastic-scale-shard-map-management.md)和[資料依存路由](sql-database-elastic-scale-data-dependent-routing.md)以 hello Entity Framework **Code First**方法。 hello [Code First-新的資料庫](http://msdn.microsoft.com/data/jj193542.aspx)EF 教學課程做為我們執行中範例整份文件。 hello 隨附這份文件的範例程式碼是彈性資料庫工具的一部分設定 hello Visual Studio 程式碼範例中的樣本。

## <a name="downloading-and-running-hello-sample-code"></a>下載並執行 hello 範例程式碼
這個發行項 toodownload hello 程式碼：

* 需要 visual Studio 2012 或更新版本。 
* 下載 hello[彈性 DB 工具適用於 Azure SQL 的實體架構整合範例](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba)從 MSDN。 將解壓縮 hello 範例 tooa 選擇的位置。
* 啟動 Visual Studio。 
* 在 Visual Studio 中，選取 [檔案] -> [開啟專案/方案]。 
* 在 [hello**開啟專案**] 對話方塊中，瀏覽您所下載的 toohello 範例並選取**EntityFrameworkCodeFirst.sln** tooopen hello 範例。 

toorun hello 範例中，您需要 toocreate 三個空白的資料庫中 Azure SQL Database:

* 分區對應管理員資料庫
* 分區 1 資料庫
* 分區 2 資料庫

一旦您已經建立這些資料庫，填寫 hello 預留位置中**Program.cs**您的 Azure SQL DB 伺服器名稱、 hello 資料庫名稱與認證 tooconnect toohello 資料庫。 建置 Visual Studio 中的 hello 方案。 Visual Studio 會下載所需的 hello NuGet 套件 hello 彈性資料庫用戶端程式庫、 Entity Framework 與暫時性錯誤處理 hello 建置程序的一部分。 請確定您的解決方案已啟用還原 NuGet 封裝。 以滑鼠右鍵按一下 hello Visual Studio 方案總管 中的 hello 方案檔，您可以啟用這項設定。 

## <a name="entity-framework-workflows"></a>Entity Framework 工作流程
Entity Framework 開發人員必須依賴 hello 下列四個工作流程 toobuild 應用程式和應用程式物件的 tooensure 持續性的其中一個： 

* **Code First （新的資料庫）**: hello EF 開發人員建立 hello 應用程式程式碼中的 hello 模型，並接著 EF hello 資料庫會從產生它。 
* **Code First （現有的資料庫）**: hello 開發人員可讓 EF hello hello 模型的應用程式程式碼產生從現有的資料庫。
* **建立第一個模型**: hello 開發人員建立 hello EF 設計工具中的 hello 模型，並接著 EF hello 資料庫會根據建立 hello 模型。
* **資料庫的第一個**: hello 開發人員會使用 EF tooling tooinfer hello 模型，從現有的資料庫。 

所有這些方法會依賴 hello DbContext 類別 tootransparently 管理資料庫連接及應用程式的資料庫結構描述。 我們會討論在 hello 件稍後詳細 hello DbContext 基底類別的不同建構函式可讓不同的層級的控制連線建立啟動載入和結構描述建立資料庫。 挑戰源自主要與 hello 連接管理功能的 hello 資料依存路由介面提供交集 hello database 連接管理 EF 所提供的 hello 事實 hello 彈性資料庫用戶端程式庫。 

## <a name="elastic-database-tools-assumptions"></a>彈性資料庫工具假設
關於詞彙定義，請參閱 [彈性資料庫工具字彙](sql-database-elastic-scale-glossary.md)。

在彈性資料庫用戶端程式庫中，您會定義應用程式資料的資料分割，稱為 Shardlet。 Shardlet 的分區化索引鍵來識別和對應的 toospecific 資料庫。 應用程式可能需要的資料庫與散發 hello shardlet tooprovide 足夠容量或指定目前的商務需求的效能。 hello 對應的分區化索引鍵值 toohello 資料庫儲存 hello 彈性資料庫用戶端應用程式開發介面所提供的分區對應。 我們將這項功能稱為 **分區對應管理**，簡稱為 SMM。 hello 分區對應也可做為 hello broker 的要求進行分區化索引鍵的資料庫連線。 我們 toothis 功能作為**資料依存路由**。 

hello 分區對應管理員防止不一致的檢視為 shardlet 資料發生並行的 shardlet 管理作業 （例如從一個分區 tooanother 重新配置的資料） 時可能發生的使用者。 toodo，hello hello 用戶端程式庫 broker hello 資料庫連接的應用程式所管理的分區對應。 這可讓 hello 分區對應功能 tooautomatically 終止資料庫連接時分區管理作業可能會影響已建立 hello 連線的 hello shardlet。 這種方法需要 toointegrate 某些 EF 的功能，例如建立新的連線，從現有的一個 toocheck 資料庫存在。 一般情況下，我們觀察已經過的 hello 標準 DbContext 建構函式只有可靠地運作可以順利複製的已關閉的資料庫連接的 EF 工作。 hello 設計原則，彈性資料庫，而是 tooonly broker 開啟連線。 其中一個可能會認為關閉連接，然後再將它傳遞 toohello EF DbContext hello 用戶端程式庫代理或許可以解決此問題。 不過，藉由關閉 hello 連接和信賴憑證者在 EF toore 開啟它，其中一個 foregoes hello 程式庫所執行的 hello 驗證和一致性檢查。 hello 移轉功能 EF，不過，使用這些連接 toomanage hello 基礎資料庫結構描述是透明的 toohello 應用程式的方式。 在理想情況下，我們會 tooretain 等結合所有這些功能從 hello 彈性資料庫用戶端程式庫和 EF hello 中的相同的應用程式。 hello 下列章節會討論這些屬性和更詳細的需求。 

## <a name="requirements"></a>需求
當使用 hello 彈性資料庫用戶端程式庫和 Entity Framework 應用程式開發介面，我們想要 tooretain hello 下列屬性： 

* **向外延展**: hello 資料 hello 分區化應用程式層的視 hello 容量需求的 hello 應用程式的 tooadd 或移除資料庫。 這表示控制 hello hello 建立和刪除的資料庫和使用 hello 彈性資料庫分區對應管理員 Api toomanage 資料庫和對應的 shardlet。 
* **一致性**: hello 應用程式會使用分區化，並使用 hello 資料依存路由的功能 hello 用戶端程式庫。 tooavoid 損毀或不正確的查詢結果，在由代理連線 hello 分區對應管理員。 這也會保留驗證和一致性。
* **Code First**: tooretain hello 的方便性，不論 EF 的程式碼的第一個範例。 在 Code First hello 應用程式中的類別會以透明的方式對應 toohello 基礎資料庫結構。 hello 應用程式程式碼會與 遮罩 hello 基礎資料庫處理所涉及的大部分層面的 DbSets 互動。
* **結構描述**：Entity Framework 會處理建立初始資料庫結構描述，以及結構描述後續透過移轉的演進。 藉由保留這些功能，調整您的應用程式就容易 hello 資料發展。 

hello 下列指導方針會指示如何 toosatisfy 使用彈性資料庫工具的第一個程式碼應用程式的需求。 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>使用 EF DbContext 的資料相依路由
資料庫與 Entity Framework 的連接通常是透過 **DbContext**的子類別管理。 從 **DbContext**衍生來建立這些子類別。 這可讓您定義您**DbSets**實作 hello 應用程式的 CLR 物件的資料庫為基礎集合。 我們可以在 hello 內容中的資料依存路由，來識別不一定是保存的其他 EF 程式碼第一個應用程式案例的一些很有幫助屬性： 

* hello 資料庫已經存在，且已註冊 hello 彈性資料庫分區對應中。 
* hello 結構描述的 hello 應用程式已經部署的 toohello 資料庫 （如下所述）。 
* 資料依存路由 toohello 資料庫的連接是由 hello 分區對應代理。 

toointegrate **DbContexts**具有資料依存路由的向外延展：

1. 建立 hello 分區對應管理員，透過 hello 彈性資料庫用戶端介面的實體資料庫的連接 
2. 自動換行以 hello hello 連接**DbContext**子類別
3. 向下 hello 連接傳入 hello **DbContext**基底類別 tooensure hello EF 端上的所有 hello 處理也會都發生。 

hello，下列程式碼範例將示範這個方法。 （此程式碼也是 hello 隨附的 Visual Studio 專案中）

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>重點
* 新的建構函式取代 hello hello DbContext 子類別中的預設建構函式 
* hello 新建構函式會採用所需的資料依存路由透過彈性資料庫用戶端程式庫的 hello 引數：
  
  * hello 分區對應 tooaccess hello 資料依存路由的介面，
  * hello 分區化索引鍵 tooidentify hello shardlet，
  * 含 hello 資料依存路由連線 toohello 分區的 hello 認證的連接字串。 
* hello 呼叫 toohello 基底類別建構函式繞道到靜態方法，會執行所有的 hello 步驟所需的資料依存路由。 
  
  * 它會使用 hello 分區對應 tooestablish 的開啟連接的 hello OpenConnectionForKey 呼叫的 hello 彈性資料庫用戶端介面。
  * hello 分區對應會建立保留 hello 指定分區化索引鍵的 hello shardlet 的 hello 開啟連接 toohello 分區。
  * 這個開啟的連接會傳遞這個連接會 toobe 而非讓 EF 自動建立新的連接使用 EF DbContext tooindicate 後 toohello 基底類別建構函式。 此方式 hello 連線已經加上 hello 彈性資料庫用戶端應用程式開發介面，讓它可以保證在分區對應管理作業的一致性。

用於 DbContext 子類別而不是在程式碼中的 hello 預設建構函式中的 hello 新建構函式。 下列是一個範例： 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

hello 新建構函式會開啟 hello 保留 hello hello shardlet hello 值所識別的資料連接 toohello 分區**tenantid1**。 hello hello 中的程式碼**使用**區塊會維持不變的 tooaccess hello **DbSet**部落格上的 hello 分區使用 EF **tenantid1**。 這會針對 hello hello 所有資料庫作業現在會使用區塊中的程式碼範圍 toohello 一個分區變更語意其中**tenantid1**會保留。 比方說，LINQ 查詢透過 hello 部落格**DbSet**就只會傳回儲存在目前的分區，hello 上的部落格，但不是 hello 是儲存在其他分區。  

#### <a name="transient-faults-handling"></a>暫時性錯誤處理
hello Microsoft Patterns & Practices 團隊發行的 hello [hello 暫時性錯誤處理應用程式區塊](https://msdn.microsoft.com/library/dn440719.aspx)。 hello 程式庫會使用彈性延展 EF 結合的用戶端程式庫。 不過，確保任何暫時性例外狀況傳回 tooa 位置，而我們可以確保該 hello 新建構函式正在使用暫時性錯誤後，讓任何新連接嘗試使用我們強制 hello 建構函式。 否則，不保證分區，且不保證 hello 連線正確連接 toohello 會維護 toohello 分區對應會發生的變更時。 

hello 下列程式碼範例說明如何 SQL 重試原則來使用周圍 hello 新**DbContext**子類別建構函式： 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** hello 在上述程式碼會定義為**SqlDatabaseTransientErrorDetectionStrategy** 10，和 5 秒的重試計數等候重試之間的時間。 這種方法很類似 toohello 指引 EF 和使用者起始的交易 (請參閱[限制以重試一次 (EF6 及更新版本) 的執行策略](http://msdn.microsoft.com/data/dn307226)。 這兩種情況需要該 hello 應用程式可以控制 hello 範圍 toowhich hello 暫時性例外狀況傳回： tooeither 重新開啟 hello 交易，或 （如下所示） 重新建立 hello 內容從使用 hello 彈性資料庫 hello 適當建構函式用戶端程式庫。

hello 需要 toocontrol 因為暫時性例外狀況傳回範圍中需要我們也會妨礙 hello 內建的 hello 使用**SqlAzureExecutionStrategy**所附 EF。 **SqlAzureExecutionStrategy**會重新開啟連線，但是不會使用**OpenConnectionForKey** ，因此略過所有執行 hello 一部分的 hello 驗證**OpenConnectionForKey**呼叫。 相反地，hello 程式碼範例會使用 hello 內建**DefaultExecutionStrategy** ，也提供的 EF。 相對於太**SqlAzureExecutionStrategy**，其運作正常的暫時性錯誤處理 hello 重試原則的組合。 hello 執行原則設定中 hello **ElasticScaleDbConfiguration**類別。 請注意，我們決定不 toouse **DefaultSqlExecutionStrategy**因為建議 toouse **SqlAzureExecutionStrategy**發生暫時性的例外狀況-這會導致 toowrong 行為所述。 Hello 不同的重試原則和 EF 的詳細資訊，請參閱[Connection Resiliency in EF](http://msdn.microsoft.com/data/dn456835.aspx)。     

#### <a name="constructor-rewrites"></a>建構函式重寫
hello 上述的程式碼範例說明 hello 預設建構函式重寫為所需的順序 toouse 資料依存路由以 hello Entity Framework 中的應用程式。 下表中的 hello 一般化這個方法 tooother 建構函式。 

| 目前的建構函式 | 重寫的資料建構函式 | 基底建構函式 | 注意事項 |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |hello 連線需要 toobe hello 分區對應和 hello 資料依存路由索引鍵的函式。 您需要的 EF tooby 行程自動連線建立，並改用 hello 分區對應 toobroker hello 連線。 |
| MyContext(string) |ElasticScaleContext(ShardMap, TKey) |DbContext(DbConnection, bool) |hello 連接是 hello 分區對應和 hello 資料依存路由索引鍵的函式。 固定的資料庫名稱或連接字串將無法運作，您會看到略過驗證的 hello 分區對應。 |
| MyContext(DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |將取得 hello 連線建立 hello 指定 hello 模型提供的檔名的分區化對應和分區化索引鍵。 將傳遞 toohello 基底 c'tor hello 編譯的模型。 |
| MyContext(DbConnection, bool) |ElasticScaleContext(ShardMap, TKey, bool) |DbContext(DbConnection, bool) |hello 連線需要 toobe 推斷從 hello 分區對應 hello 索引鍵。 （除非該輸入已經使用 hello 分區對應和 hello 金鑰），不能提供它做為輸入。 將傳遞 hello 布林值。 |
| MyContext(string, DbCompiledModel) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel) |DbContext(DbConnection, DbCompiledModel, bool) |hello 連線需要 toobe 推斷從 hello 分區對應 hello 索引鍵。 （除非已使用該輸入，hello 分區對應和 hello 金鑰），不能提供它做為輸入。 將傳遞 hello 編譯的模型。 |
| MyContext(ObjectContext, bool) |ElasticScaleContext(ShardMap, TKey, ObjectContext, bool) |DbContext(ObjectContext, bool) |hello 新建構函式需要 tooensure hello 當做輸入傳遞 ObjectContext 中的任何連接是重新路由的 tooa 連接受彈性延展。 ObjectContexts 詳細的討論已超出本文件 hello 範圍。 |
| MyContext(DbConnection, DbCompiledModel,bool) |ElasticScaleContext(ShardMap, TKey, DbCompiledModel, bool) |DbContext(DbConnection, DbCompiledModel, bool); |hello 連線需要 toobe 推斷從 hello 分區對應 hello 索引鍵。 （除非該輸入已經使用 hello 分區對應和 hello 金鑰），無法提供 hello 連接做為輸入。 模型和布林值會傳遞 toohello 基底類別建構函式。 |

## <a name="shard-schema-deployment-through-ef-migrations"></a>透過 EF 移轉的分區結構描述部署
管理自動的結構描述是方便 hello Entity Framework 所提供。 Hello 在內容中使用彈性資料庫工具的應用程式，我們想 tooretain 此功能 tooautomatically 佈建 hello 結構描述建立 toonewly 分區時的資料庫會加入 toohello 分區化應用程式。 hello 主要使用案例是在 hello 資料層分區化應用程式使用 EF tooincrease 容量。 信賴憑證者的結構描述管理 EF 的功能與 EF 上建置分區化應用程式減少 hello 資料庫管理工作。 

透過 EF 移轉的結構描述部署在 **未開啟的連接**上表現最好。 這是相較之下 toohello 案例資料依存路由依賴 hello 彈性資料庫用戶端應用程式開發介面所提供的 hello 開啟連接。 另一項差異是 hello 一致性需求： 所有資料依存路由連線 tooprotect 針對並行分區對應管理的理想 tooensure 一致性，同時它不是初始的結構描述部署 tooa 新資料庫的相關問題具有尚未在 hello 分區對應中，尚未註冊，且尚未在已配置 toohold shardlet。 我們因此可依賴此案例中，做為相對於 toodata 依存路由規則的資料庫連接。  

這會導致 tooan 方法其中透過 EF 移轉的結構描述部署與緊密結合 hello hello 新的資料庫註冊為 hello 應用程式的分區對應中的分區。 這會依賴 hello 下列必要條件： 

* 已建立 hello 資料庫。 
* hello 資料庫是空的-它會保留任何的使用者結構描述和任何使用者資料。
* hello 資料庫尚未無法透過 hello 彈性資料庫用戶端應用程式開發介面資料依存路由的存取。 

這些先決條件備妥，我們可以建立一般未開啟**SqlConnection** tookick 關閉結構描述部署的 EF 移轉。 hello，下列程式碼範例將示範這個方法。 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


這個範例會顯示 hello 方法**RegisterNewShard**暫存器 hello 在 hello 分區對應中，分區部署 hello 透過 EF 移轉的結構描述和儲存的分區化索引鍵 toohello 分區對應。 它依賴 hello 的建構函式**DbContext**子類別 (**ElasticScaleContext** hello 範例中)，使用 SQL 連接字串做為輸入。 這個建構函式的 hello 程式碼是明瞭，為下列範例所示的 hello: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

其中一個可能使用 hello hello 建構函式繼承自 hello 基底類別版本。 但 hello EF 預設初始設定式的 hello 程式碼需要 tooensure 在連接時使用。 因此 hello 簡短繞道至 hello hello 連接字串 hello 基底類別建構函式呼叫之前的靜態方法。 請注意，分區的 hello 註冊應該執行不發生衝突的 EF hello 初始設定式設定不同的應用程式定義域或處理序 tooensure 中。 

## <a name="limitations"></a>限制
這份文件中所述的 hello 方法需要有幾項限制： 

* 使用 EF 應用程式**LocalDb**使用彈性資料庫用戶端程式庫之前先 toomigrate tooa 一般 SQL Server 資料庫。 使用 **LocalDb**時，無法透過分區化與 Elastic Scale 來相應放大應用程式。 請注意，仍可使用 **LocalDb**來開發。 
* 表示資料庫結構描述變更的任何變更 toohello 應用程式需要透過在所有分區的 EF 移轉 toogo。 本文件的 hello 範例程式碼不會示範如何 toodo 這。 請考慮更新資料庫具有 ConnectionString 參數 tooiterate 透過所有分區。擷取 hello T-SQL 指令碼或暫止移轉使用 Update-database 搭配 hello hello-指令碼選項，並套用 hello T-SQL 指令碼 tooyour 分區。  
* 指定要求，則會假設其資料庫處理的所有包含在單一分區中的 hello hello 要求所提供的分區化索引鍵識別。 不過，這項假設不一定永遠成立。 例如，當不可能 toomake 分區化索引鍵使用。 tooaddress hello，用戶端程式庫提供 hello **MultiShardQuery**類別會實作抽象的查詢數個分區的連線。 學習 toouse hello **MultiShardQuery**搭配 EF 超出本文的 hello 範圍

## <a name="conclusion"></a>結論
Hello 這份文件中所述的步驟，透過 EF 應用程式可以使用 hello 彈性資料庫用戶端程式庫的功能資料依存路由重構建構函式的 hello **DbContext** hello EF 中使用的子類別應用程式。 此限制 hello 變更所需 toothose 位置**DbContext**類別已存在。 此外，EF 應用程式可以繼續從自動結構描述部署 toobenefit 結合叫用 hello 必要 EF 移轉，而 hello 註冊新的分區和 hello 分區對應中的對應的 hello 步驟。 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
