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
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>如何 toouse 批次處理 tooimprove SQL Database 應用程式效能
批次處理作業 tooAzure SQL Database 會大幅改善 hello 效能和延展性的應用程式。 順序 toounderstand hello 好處，在這篇文章 hello 第一個部分涵蓋比較循序和批次要求 tooa SQL Database 的一些範例測試結果。 hello hello 文章的其餘部分會顯示 hello 技術、 案例和考量 toohelp 您 toouse 批次已成功將 Azure 應用程式中。

## <a name="why-is-batching-important-for-sql-database"></a>為什麼批次處理對 SQL Database 很重要？
呼叫 tooa 遠端服務的批次處理是已知的策略，提升效能和延展性。 都那里固定的處理成本 tooany 互動與遠端服務，例如序列化、 網路傳輸和還原序列化。 將許多個別交易包裝成單一批次可將這些成本降到最低。

本文中，我們想要 tooexamine 各種 SQL Database 批次處理策略和案例。 雖然這些策略也是使用 SQL Server 的內部部署應用程式很重要的有多種原因所造成的反白顯示 hello 的批次處理使用 SQL Database:

* 沒有可能會比較高的網路延遲存取 SQL 資料庫，特別是如果您要從外部 hello 存取 SQL 資料庫相同的 Microsoft Azure 資料中心。
* hello 多租用戶特性為 SQL 資料庫，表示 hello 效率的 hello 資料存取層相互關聯 toohello hello 資料庫的整體延展性。 SQL 資料庫必須防止任何單一租用戶/使用者獨佔資料庫資源 toohello 而妨礙其他租用戶。 在回應 toousage 超過預先定義的配額，SQL Database 可以減少輸送量或是以節流例外回應。 效率，例如，批次，可讓您 toodo 達到這些限制前於 SQL Database 的更多工作。 
* 在使用多個資料庫 (分區化) 的架構下，批次處理也很有效益。 每個資料庫單元與您互動的 hello 效率仍然是整體延展性的關鍵因素。 

使用 SQL Database hello 優點的其中一個是您不需要 toomanage hello 伺服器主機 hello 資料庫。 不過，此受管理的基礎結構也表示您必須以不同方式的相關資料庫最佳化 toothink。 您可以不再尋找 tooimprove hello 資料庫硬體或網路基礎結構。 Microsoft Azure 會控制那些環境。 您可以控制 hello 主要區域是您的應用程式與 SQL Database 之間的互動方式。 批次處理屬於這些最佳化作法之一。 

hello 紙張 hello 第一個部分會檢查.NET 應用程式使用 SQL Database 的各種批次技術。 hello 最後兩節討論批次處理方針和案例。

## <a name="batching-strategies"></a>批次處理策略
### <a name="note-about-timing-results-in-this-topic"></a>有關本主題中計時結果的注意事項
> [!NOTE]
> 結果並不是基準，目的只是 tooshow**相對效能**。 計時至少根據 10 個測試回合的平均值。 作業插入至空的資料表。 這些測試測量的 V12 之前，所以它們不一定對應使用 hello 新 V12 資料庫中，您可能會遇到的 toothroughput[服務層](sql-database-service-tiers.md)。 批次技術 hello hello 相對效益應該類似。
> 
> 

### <a name="transactions"></a>交易
似乎奇怪 toobegin 檢視討論交易批次處理。 但 hello 使用用戶端交易會對具有難以察覺的伺服器端批次處理效果，可改善效能。 交易可以加入只幾行程式碼，讓使用者提供快速 tooimprove 循序作業效能。

請考慮下列 C# 程式碼，其中包含一連串的 insert hello 和簡單的資料表上的 update 作業。

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

hello 下列 ADO.NET 程式碼，以循序方式執行這些作業。

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

hello 最佳方式 toooptimize 這段程式碼是 tooimplement 某種形式的用戶端批次處理這些呼叫。 但是 hello 序列呼叫包裝在交易中沒有簡單的方式 tooincrease hello 這個程式碼的效能。 以下是 hello 相同的程式碼改成使用交易。

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

這兩個範例實際上都使用交易。 在 hello 第一個範例中，每個個別的呼叫是隱含的交易。 在 hello 第二個範例中，明確的交易中包裝所有 hello 呼叫。 每個 hello 文件以 hello[預先寫入交易記錄檔](https://msdn.microsoft.com/library/ms186259.aspx)，hello 交易認可時，記錄檔記錄會排清的 toohello 磁碟。 因此只要在交易中包含多個呼叫，hello 寫入 toohello 交易記錄檔可能會延遲 hello 交易認可之前。 作用中，您要啟用 hello 寫入 toohello 伺服器的交易記錄的批次。

hello 下表顯示一些臨機操作測試結果。 hello 相同循序插入與交易不會執行 hello 測試。 如需詳細的觀點來看，hello 第一組測試從遠端執行從膝上型電腦 toohello 資料庫在 Microsoft Azure 中。 hello 第二組測試從執行雲端服務和資料庫位在 hello 相同 Microsoft Azure 資料中心 （美國西部）。 hello 下表顯示 hello 持續時間以毫秒為單位的逾時或無交易的循序插入。

**在內部部署 tooAzure**:

| 作業 | 無交易 (毫秒) | 交易 (毫秒) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**Azure tooAzure （相同資料中心）**:

| 作業 | 無交易 (毫秒) | 交易 (毫秒) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> 結果並不是基準。 請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。
> 
> 

根據 hello 先前的測試結果，將單一作業包裝在交易中其實會降低效能。 但隨著您增加 hello 在單一交易中的作業數目時，會變成更標示 hello 效能改進。 hello Microsoft Azure 資料中心內發生的所有作業時，也更明顯 hello 效能差異。 hello 使用從外部 hello Microsoft Azure 資料中心的 SQL Database 的延遲增加減低使用交易所 hello 效能提升。

雖然 hello 使用交易可以提高效能，繼續太[觀察交易和連接的最佳作法](https://msdn.microsoft.com/library/ms187484.aspx)。 Hello 工作完成後，請保留 hello 交易越短越好，並關閉 hello 資料庫連接。 hello hello 前一個範例中使用陳述式可確保 hello 連接已關閉時完成 hello 後續程式碼區塊。

hello 前一個範例示範您可以加入本機交易 tooany ADO.NET 程式碼透過兩行。 交易提供快速的方式，tooimprove hello 效能的程式碼，可循序插入、 更新和刪除作業。 不過，為了 hello 最快效能，請考慮變更 hello 程式碼進一步 tootake 用戶端批次的優點，例如資料表值參數。

如需 ADO.NET 中的交易的詳細資訊，請參閱 [ADO.NET 中的本機交易](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions)。

### <a name="table-valued-parameters"></a>資料表值參數
資料表值參數支援使用者定義資料表類型做為 Transact-SQL 陳述式、預存程序和函數中的參數。 此用戶端批次處理技術可讓您 toosend 內 hello 資料表值參數資料的多個資料列。 toouse 資料表值參數，會先定義資料表類型。 hello 下列 TRANSACT-SQL 陳述式建立資料表類型名為**MyTableType**。

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


在程式碼中，您會建立**DataTable**以 hello 完全相同的名稱和類型的 hello 資料表類型。 將這個 **DataTable** 傳入文字查詢或預存程序呼叫中的參數。 hello 下例示範這項技術：

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

Hello 上述範例中，在 hello **SqlCommand**物件是資料表值參數，會將資料列 **@TestTvp** 。 先前建立的 hello **DataTable** hello toothis 參數指派給物件**SqlCommand.Parameters.Add**方法。 批次處理 hello 插入其中一個呼叫會大幅增加 hello 效能比循序插入。

tooimprove hello 前一個範例，會使用預存程序，而不是以文字為基礎的命令。 hello 下列 TRANSACT-SQL 命令建立預存程序採用 hello **SimpleTestTableType**資料表值參數。

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

然後變更 hello **SqlCommand** hello 前一個範例 toohello 後面的程式碼中宣告的物件。

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

在大部分情況下，資料表值參數的效能同於或高於其他批次處理技術。 資料表值參數通常較適合，因為比其他選項更有彈性。 例如，SQL 大量複製等其他技術只允許 hello 插入新資料列。 但使用資料表值參數，您可以使用邏輯在 hello 預存程序 toodetermine 哪些資料列會更新和插入。 hello 資料表類型也可以修改的 toocontain 表示 hello 指定資料列應該是插入、 更新或刪除的 「 作業 」 資料行。

下表中的 hello 顯示 hello 使用資料表值參數的臨機操作測試結果，以毫秒為單位。

| 作業 | 在內部部署 tooAzure （毫秒） | Azure 相同資料中心 (毫秒) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10000 |23830 |3586 |

> [!NOTE]
> 結果並不是基準。 請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。
> 
> 

從批次的 hello 效能提升會立即出現。 在上一個循序測試 hello，1000 次作業花費 129 秒外部 hello 資料中心和從 hello 資料中心內的 21 秒。 但是使用資料表值參數，1000 次作業會採用只有 2.6 秒 hello 資料中心以外和 hello 資料中心內則只需 0.4 秒。

如需資料表值參數的詳細資訊，請參閱 [資料表值參數](https://msdn.microsoft.com/library/bb510489.aspx)。

### <a name="sql-bulk-copy"></a>SQL 大量複製
SQL 大量複製是另一個方式 tooinsert 大量資料到目標資料庫。 .NET 應用程式可以使用 hello **SqlBulkCopy**類別 tooperform 大量插入作業。 **SqlBulkCopy**函式 toohello 命令列工具，在類似**Bcp.exe**，或使用 TRANSACT-SQL 陳述式，hello **BULK INSERT**。 hello 下列程式碼範例示範 toobulk 複製 hello hello 來源中的資料列**DataTable**，資料表、 在 SQL Server，MyTable toohello 目的地資料表。

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

在某些情況下，大量複製比資料表值參數更適合。 請參閱資料表值參數與 BULK INSERT 作業 hello 主題中的 hello 比較表[資料表值參數](https://msdn.microsoft.com/library/bb510489.aspx)。

hello 下列臨機操作測試結果顯示 hello 效能與批次處理**SqlBulkCopy**以毫秒為單位。

| 作業 | 在內部部署 tooAzure （毫秒） | Azure 相同資料中心 (毫秒) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10000 |21605 |2737 |

> [!NOTE]
> 結果並不是基準。 請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。
> 
> 

在較小的批次大小 hello 使用資料表值參數的效能勝過 hello **SqlBulkCopy**類別。 不過， **SqlBulkCopy** hello 測試 1,000 和 10,000 個資料列的執行速度比資料表值參數 12-31%。 例如資料表值參數， **SqlBulkCopy**是不錯的選項，批次的插入，尤其是與 toohello 效能的非批次作業。

如需 ADO.NET 中的大量複製的詳細資訊，請參閱 [SQL Server 中的大量複製作業](https://msdn.microsoft.com/library/7ek5da1a.aspx)。

### <a name="multiple-row-parameterized-insert-statements"></a>多資料列參數化 INSERT 陳述式
小批次的一種替代方法是 tooconstruct 大型參數化 INSERT 陳述式會插入多個資料列。 hello，下列程式碼範例示範這項技術。

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


此範例的目的在於 tooshow hello 基本概念。 比較真實的案例會同時循環所需的 hello 實體 tooconstruct hello 查詢字串和 hello 命令參數。 最多只能 tooa 2100 查詢參數，因此這會限制 hello 總數，這種方式可以處理的資料列的總數。

下列臨機操作測試結果顯示 hello 效能這種類型的 insert 陳述式，以毫秒為單位的 hello。

| 作業 | 資料表值參數 (毫秒) | 單一陳述式 INSERT (毫秒) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> 結果並不是基準。 請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。
> 
> 

如果批次少於 100 的資料列，這種方法會稍微快一些。 雖然 hello 改進很小，這項技術是另一個選項，可能也在特定應用程式案例中運作。

### <a name="dataadapter"></a>DataAdapter
hello **DataAdapter**類別可讓您 toomodify**資料集**物件，然後送出 hello 變更做為 INSERT、 UPDATE 和 DELETE 作業。 如果您使用 hello **DataAdapter**在這種方式，是很重要，個別呼叫 toonote 會針對每個相異的作業。 tooimprove 效能，使用 hello **UpdateBatchSize**屬性 toohello 數目應該同時批次處理的作業。 如需詳細資訊，請參閱 [使用 Dataadapter 執行批次作業](https://msdn.microsoft.com/library/aadf8fk2.aspx)。

### <a name="entity-framework"></a>Entity Framework
Entity Framework 目前不支援批次處理。 Hello 社群中的不同開發人員嘗試 toodemonstrate 因應措施，例如覆寫 hello **SaveChanges**方法。 但 hello 解決方案通常 toohello 複雜和自訂應用程式和資料模型。 hello Entity Framework codeplex 專案目前沒有這項功能要求上的討論頁。 tooview 本討論中，請參閱[設計會議記錄-2012 年 8 月 2 日](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012)。

### <a name="xml"></a>XML
為求完整起見，我們覺得很重要的 tootalk xml 做為批次策略。 不過，hello 使用 XML 沒有任何優於其他方法和幾個缺點。 hello 方法是類似 tootable 值的參數，但 XML 檔案，或是字串傳遞 tooa 預存程序，而不是使用者定義的資料表。 hello 預存程序會剖析 hello 預存程序中的 hello 命令。

Toothis 方法有幾個缺點：

* 處理 XML 很麻煩又容易出錯。
* 剖析 hello XML hello 資料庫上的可能需要大量 CPU。
* 在大部分情況下，這種方法比資料表值參數更慢。

基於這些理由，不建議 hello 使用 XML 進行批次查詢。

## <a name="batching-considerations"></a>批次處理考量
hello 下列各節提供 hello 使用批次作業中 SQL Database 應用程式的詳細指引。

### <a name="tradeoffs"></a>權衡取捨
根據您的架構而定，批次處理可能需要在效能和恢復功能之間有所取捨。 例如，請考慮 hello 案例中，您的角色異常中斷。 如果您遺失一個資料列，hello 影響會小於遺失大批尚未認可的資料列的大型批次的 hello 影響。 當您在指定的時段傳送 toohello 資料庫之前，先緩衝處理資料列時，沒有更大的風險。

這些權衡取捨，因為評估您要批次處理 hello 的作業類型。 對於較不重要的資料，應該更積極地批次處理 (較大的批次和較長的時間範圍)。

### <a name="batch-size"></a>批次大小
在我們的測試時通常不利用 toobreaking 大型批次分成小塊。 事實上，這樣分割通常會導致效能比提交單一大型批次更慢。 例如，假設您想要 tooinsert 1000 個資料列。 hello 下表顯示要花多久 toouse 資料表值參數 tooinsert 1000 列分成較小的批次時。

| 批次大小 | 反覆運算次數 | 資料表值參數 (毫秒) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> 結果並不是基準。 請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。
> 
> 

您可以看見 hello 1000 個資料列的最佳效能是 toosubmit 它們一次。 在其他測試中 （此處未顯示） 時發生輕微的效能改善 toobreak 10000 的資料列批次分成兩個批次為 5000。 但這些測試的 hello 資料表結構描述相當簡單，所以您必須執行上測試您的特定資料和批次大小 tooverify 這些研究結果。

另一個因素 tooconsider 是 hello 總批次變得太大，如果 SQL 資料庫可能會節流並拒絕 toocommit hello 批次。 Hello 獲得最佳結果，測試特定案例 toodetermine，如果沒有理想的批次大小。 請根據效能或錯誤的執行階段 tooenable 快速調整設定 hello 批次大小。

最後，平衡 hello hello 批次大小與 hello 與批次處理風險。 如果暫時性錯誤或 hello 角色失敗，請考慮 hello 或 hello hello 批次中的資料遺失的重試 hello 作業的結果。

### <a name="parallel-processing"></a>平行處理
如果您 hello 方式減少 hello 批次大小，而使用多個執行緒 tooexecute hello 工作？ 同樣地，我們的測試指出數個較小的多執行緒批次通常表現得比單一大型批次更差。 hello 下列測試嘗試 tooinsert 1000 個資料列中一個或多個平行批次。 此測試指出同時有多個批次實際上會降低效能。

| 批次大小 [反覆運算次數] | 兩個執行緒 (毫秒) | 四個執行緒 (毫秒) | 六個執行緒 (毫秒) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> 結果並不是基準。 請參閱 hello[有關本主題中的計時結果注意事項](#note-about-timing-results-in-this-topic)。
> 
> 

有 hello 效能降低的原因可能到期 tooparallelism:

* 同時有多個網路呼叫，而不只一個。
* 對單一資料表執行多個作業會導致爭用和鎖定。
* 多執行緒處理會引起額外負荷。
* 開啟多個連接的 hello 費用超過 hello 平行處理的效益。

如果您以不同的資料表或資料庫目標，則可能 toosee 這項策略而提升的一些效能。 資料庫分區化或同盟就是適合這種方法的案例。 多個資料庫與路由不同資料 tooeach 資料庫，則會使用分區化。 如果每個小的批次即將 tooa 不同的資料庫，然後以平行方式執行 hello 作業可能會更有效率。 不過，hello 獲得效能未明顯 toouse 決策 toouse 資料庫分區化方案中的 hello 基礎。

在某些設計中，平行執行較小的批次可以在負載不足的系統中改善要求輸送量。 在此情況下，即使它是快速 tooprocess 單一較大的批次時，處理多個批次，以平行方式可能會更有效率。

如果您使用平行執行，請考慮控制 hello 最大工作者執行緒數目。 數量較少可以減少爭用，並加快執行時間。 此外，請考慮 hello 這會在連接和交易 hello 目標資料庫的額外負載。

### <a name="related-performance-factors"></a>相關的效能因素
資料庫效能的一般指引也會影響批次處理。 例如，如果資料表具有大型的主索引鍵或許多非叢集索引，插入效能會降低。

如果資料表值參數使用預存程序，您可以使用 hello 命令**SET NOCOUNT ON** hello 程序的 hello 開頭。 這個陳述式會隱藏 hello 傳回 hello hello 程序中的 hello 受影響的資料列計數。 不過，在我們的測試，hello 使用**SET NOCOUNT ON**可能是沒有任何作用或是會降低效能。 hello 測試預存程序很簡單，只有單一**插入**命令從 hello 資料表值參數。 此陳述式可能有益於更複雜的預存程序。 但是，請勿假設該新增**SET NOCOUNT ON** tooyour 預存程序會自動改善效能。 toounderstand hello 效果，請測試預存程序逾時或無 hello **SET NOCOUNT ON**陳述式。

## <a name="batching-scenarios"></a>批次處理案例
hello 下列各節說明如何在三個應用程式案例 toouse 資料表值參數。 hello 第一個案例示範緩衝和批次處理可以運作方式在一起。 hello 第二個案例會執行單一預存程序呼叫中的主檔/明細作業，以提高效能。 hello 最後一個案例示範如何在 「 更新插入 」 作業中的 toouse 資料表值參數。

### <a name="buffering"></a>緩衝處理
雖然有些案例很明顯適合使用批次處理，但也有許多案例可以藉由延遲處理來利用批次處理。 不過，延遲處理也會帶來更 hello 未預期的錯誤事件中的 hello 資料遺失的風險。 它是重要的 toounderstand 此風險並考慮 hello 的結果。

例如，請考慮追蹤 hello 巡覽記錄的每個使用者的 web 應用程式。 每個頁面要求 hello 應用程式可以進行資料庫呼叫 toorecord hello 使用者的頁面檢視。 但是，可藉由 hello 使用者的導覽活動緩衝處理，然後將此資料 toohello 資料庫傳送批次中較高的效能和延展性。 您可以觸發 hello 所經過的時間和 （或） 緩衝區大小的資料庫更新。 例如，規則無法指定應該在 20 秒，或當 hello 緩衝區達到 1000 個項目之後處理 hello 該批次。

hello 下列程式碼範例使用[Reactive Extensions-Rx](https://msdn.microsoft.com/data/gg577609) tooprocess 緩衝處理的監視類別所引發的事件。 當 hello 緩衝區填滿或達到逾時，使用者資料的 hello 批次傳送 toohello 資料庫與資料表值參數。

hello 下列 NavHistoryData 類別模型 hello 使用者導覽詳細資料。 其中包含 hello 使用者識別項等基本資訊、 hello URL 存取，而且 hello 存取時間。

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

hello NavHistoryDataMonitor 類別會負責緩衝 hello 使用者瀏覽資料 toohello 資料庫。 它包含 RecordUserNavigationEntry 方法，以引發 **OnAdded** 事件做為回應。 hello 下列程式碼顯示 hello 建構函式邏輯，會使用 Rx toocreate 根據 hello 事件可觀察的集合。 然後會使用 hello 緩衝區方法訂閱 toothis 可觀察的集合。 hello 多載會指定應傳送該 hello 緩衝區，每隔 20 秒或 1000 個項目。

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

hello 處理常式將所有緩衝的 hello 項目轉換成資料表值的類型，然後將該處理程序 hello 批次傳送此類型 tooa 預存程序。 hello 下列程式碼顯示 hello hello NavHistoryDataEventArgs 和 hello NavHistoryDataMonitor 類別的完整定義。

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

toouse 這個緩衝類別 hello 應用程式建立靜態 NavHistoryDataMonitor 物件。 使用者存取頁面時，每次 hello 應用程式呼叫 hello NavHistoryDataMonitor.RecordUserNavigationEntry 方法。 hello 緩衝邏輯繼續 tootake care of 傳送批次中的這些項目 toohello 資料庫。

### <a name="master-detail"></a>主要/詳細架構
資料表值參數適用於簡單的 INSERT 案例。 不過，它可以是更具挑戰性 toobatch 插入牽涉到多個資料表。 hello 「 主檔/明細 」 案例中是一個好範例。 hello 主要資料表識別 hello 主要實體。 一或多個明細資料表則存放有關 hello 實體的詳細資料。 在此案例中，外部索引鍵關聯性會強制 hello 關聯性的詳細資料 tooa 唯一主要實體。 假設有一個簡化版的 PurchaseOrder 資料表及其相關聯的 OrderDetail 資料表。 hello 下列 TRANSACT-SQL 會建立具有四個資料行的 hello PurchaseOrder 資料表： OrderID、 OrderDate、 CustomerID 及狀態。

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

每筆訂單包含一或多個產品採購。 Hello PurchaseOrderDetail 資料表中擷取這項資訊。 hello 下列 TRANSACT-SQL 會建立具有五個資料行的 hello PurchaseOrderDetail 資料表： OrderID、 OrderDetailID、 ProductID、 UnitPrice 和 OrderQty。

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

hello PurchaseOrderDetail 資料表中的 hello OrderID 資料行必須從 hello PurchaseOrder 資料表參考的順序。 hello 遵循的外部索引鍵定義強制這個限制。

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

順序 toouse 資料表值參數，您必須針對每個目標資料表的一種使用者定義資料表類型。

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

然後，定義一個可接受這幾種資料表的預存程序。 此程序可讓應用程式 toolocally 批次的一組訂單和訂單詳細資料的單一呼叫中。 hello 下列 TRANSACT-SQL 提供 hello 這個採購單範例的完整預存程序宣告。

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

在此範例中，hello 本機定義@IdentityLink資料表會儲存新插入的 hello 資料列的 hello 實際訂單編號值。 這些訂單識別碼會與不同 hello 暫時訂單編號的值在 hello@orders和@details資料表值參數。 基於這個理由，hello@IdentityLink資料表再 hello OrderID 值會從連線 hello @orders toohello 真實 OrderID 的參數值 hello hello PurchaseOrder 資料表中的新資料列。 這個步驟之後，hello@IdentityLink資料表可促進插入 hello 訂單詳細資料，以 hello 滿足 hello foreign key 條件約束的實際 OrderID。

從程式碼或其他 Transact-SQL 呼叫中，都可以使用這個預存程序。 請參閱 hello 資料表值參數的程式碼範例的這份文件。 下列 TRANSACT-SQL hello 顯示 toocall hello sp_InsertOrdersBatch 的方式。

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

這個解決方案讓每個批次 toouse 一組從 1 開始的訂單編號值。 這些暫存 OrderID 值描述 hello hello 的批次中的關聯性，但是 hello hello 插入作業時就會判斷 hello 實際的訂單編號值。 您可以執行 hello 相同的陳述式 hello 前一個範例中重複，並產生唯一的訂單 hello 資料庫中。 因此，使用這種批次技術時，請考慮新增更多程式碼或資料庫邏輯，以防止訂單重複。

此範例示範即使是更複雜的資料庫作業，例如主要/詳細架構作業，也都可以透過資料表值參數進行批次處理。

### <a name="upsert"></a>UPSERT
另一個批次處理案例涉及同時更新現有的資料列和插入新資料列。 這項作業有時候會參考的 tooas"UPSERT"（更新 + 插入） 作業。 而不是執行個別的呼叫 tooINSERT 和更新，hello MERGE 陳述式會是最適合的 toothis 工作。 hello MERGE 陳述式可以同時執行插入和更新作業的單一呼叫中。

資料表值參數可以搭配 hello MERGE 陳述式 tooperform 更新和插入。 例如，請考慮簡化的員工資料表，其中包含下列資料行的 hello: EmployeeID、 FirstName、 LastName、 SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

在此範例中，您可以使用該 hello SocialSecurityNumber 是唯一 tooperform 合併多名員工的 hello 事實。 首先，建立 hello 使用者定義資料表類型：

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

接下來，建立預存程序，或撰寫程式碼會使用 hello MERGE 陳述式 tooperform hello 更新和插入。 hello 下列範例會使用 hello MERGE 陳述式資料表值參數， @employees，EmployeeTableType 型別。 hello 的 hello 內容@employees此處未顯示資料表。

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

如需詳細資訊，請參閱 hello 文件集和 hello MERGE 陳述式的範例。 相同的工作無法執行多個步驟中的 hello 預存程序呼叫，以個別的 INSERT 和 UPDATE 作業，雖然 hello MERGE 陳述式會更有效率。 資料庫程式碼也可以建構 TRANSACT-SQL 呼叫使用直接而不需要針對插入和更新的兩個資料庫呼叫 hello MERGE 陳述式。

## <a name="recommendation-summary"></a>建議摘要
hello 下列清單提供 hello 批次處理本主題所討論的建議的摘要：

* 使用緩衝和批次處理 tooincrease hello 效能和延展性的 SQL Database 應用程式。
* 了解批次處理/緩衝處理與復原之間的權衡取捨完全 hello。 在角色失敗時，遺失的業務關鍵資料的未處理的批次的 hello 風險程度可能會超過 hello 批次作業的效能優勢。
* 嘗試 tookeep 所有呼叫 toohello 資料庫內的單一資料中心 tooreduce 延遲。
* 如果您選擇單一批次處理技術，資料表值參數提供 hello 最佳效能和彈性。
* 最快的 hello 插入效能，請遵循這些一般指導方針，但測試您的案例：
  * 如果 < 100 個資料列，使用單一參數化 INSERT 命令。
  * 如果 < 1000 個資料列，使用資料表值參數。
  * 如果 >= 1000 個資料列，使用 SqlBulkCopy。
* 針對更新和刪除作業，判斷 hello hello 資料表參數中的每個資料列上的正確作業的預存程序邏輯中使用資料表值參數。
* 批次大小的指導方針：
  * 使用 hello 最大批次大小對您的應用程式和商務需求的有意義。
  * 平衡 hello 效能提升的大型批次 hello 的暫時性或災難性失敗的風險。 重試次數的 hello 結果或 hello hello 批次中的資料遺失是什麼？ 
  * 測試 hello 最大批次大小 tooverify，SQL Database 不會拒絕它。
  * 建立控制批次處理，例如 hello 批次大小或緩衝時間間隔 hello 組態設定。 這些設定提供彈性。 您可以變更批次處理行為在生產環境中的，而不必重新部署 hello 雲端服務的 hello。
* 避免在一個資料庫的單一資料表上平行執行批次。 如果您選擇 toodivide 單一批次多個背景工作執行緒上，執行測試 toodetermine hello 理想的執行緒數目。 超過未確定的臨界值之後，更多的執行緒只會降低效能，不會提高效能。
* 在更多案例下，考慮依大小和時間緩衝來實作批次處理。

## <a name="next-steps"></a>後續步驟
本文著重於資料庫設計和編碼技術相關 toobatching 可以改善您的應用程式效能和延展性。 但這只是整體策略中的一個因素。 如需詳細的方式 tooimprove 效能和延展性，請參閱[單一資料庫的 Azure SQL Database 效能指引](sql-database-performance-guidance.md)和[彈性集區的價格和效能考量](sql-database-elastic-pool-guidance.md)。

