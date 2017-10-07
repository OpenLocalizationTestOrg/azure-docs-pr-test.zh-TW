---
title: "aaaAzure SQL Database 效能調整指引 |Microsoft 文件"
description: "這篇文章可協助您判斷哪一個應用程式的服務層 toochoose。 它也會建議方式 tootune 您充分利用 Azure SQL Database 的應用程式 tooget hello。"
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>微調 Azure SQL Database 中的資料庫效能

Azure SQL Database 提供[建議](sql-database-advisor.md)，您可以使用 tooimprove 效能，您的資料庫，或是您可以讓 Azure SQL Database[隨著 tooyour 應用程式的自動調整](sql-database-automatic-tuning.md)並套用變更可改善您的工作負載的效能。

在您不需要任何適用的建議，而您仍效能問題，您可能會使用下列方法 tooimprove 演唱 hello:
1. 增加[服務層](sql-database-service-tiers.md)並提供更多資源 tooyour 資料庫。
2. 微調您的應用程式，並套用一些可以改善效能的最佳做法。 
3. 變更索引和 toomore 有效率地處理資料的查詢來微調 hello 資料庫。

這些是手動方法，因為您需要 toodecide 什麼[服務層](sql-database-service-tiers.md)會選擇，或您會需要 toorewrite 應用程式或資料庫程式碼並部署 hello 變更。

## <a name="increasing-performance-tier-of-your-database"></a>增加資料庫的效能層級

Azure SQL Database 提供四個[服務層](sql-database-service-tiers.md)供您選擇：基本、標準、進階及進階 RS (以資料庫輸送量單位 (簡稱 [DTU](sql-database-what-is-a-dtu.md)) 測量效能)。 每個服務層嚴格隔離 hello 資源可以使用 SQL database，與可保證該服務層級的效能預測性。 在本文中，我們會提供可協助您選擇您的應用程式的 hello 服務層的指引。 我們也將討論您可以微調您充分利用 Azure SQL Database 的應用程式 tooget hello。

> [!NOTE]
> 本文著重在 Azure SQL Database 中單一資料庫的效能指引。 如需效能指引相關的 tooelastic 集區，請參閱[彈性集區的價格和效能考量](sql-database-elastic-pool-guidance.md)。 不過請注意，您可以用來套用微調建議的彈性集區，在此發行項 toodatabases hello 的許多，並取得類似的效能優勢。
> 

* **基本**: hello 基本服務層提供良好的效能可預測性的每個資料庫、 小時內的小時。 在基本資料庫中，會有足夠的資源可在不會有多個並行要求的小型資料庫中支援良好的效能。 使用基本服務層時的一般使用案例如下：
  * **您剛開始使用 Azure SQL Database**。 開發中的應用程式通常不需要很高的效能等級。 基本資料庫的價格便宜，是適合用來開發或測試資料庫的理想環境。
  * **您的資料庫只有單一使用者**。 將單一使用者與資料庫相關聯的應用程式通常沒有高度的並行存取和效能需求。 這些應用程式是 hello Basic 服務層的候選項目。
* **標準**: hello Standard 服務層提供更佳的效能可預測性，並提供良好的效能有多個並行要求的詳細資訊，例如工作群組和 web 應用程式的資料庫。 當您使用標準服務層資料庫時，您可以根據可預測的效能，每分鐘調整資料庫應用程式的大小。
  * **您的資料庫有多個並行要求**。 一次服務多名使用者的應用程式通常需要較高的效能等級。 例如，工作群組或 web 應用程式的支援多個並行查詢的低 toomedium IO 流量需求十分適合 hello Standard 服務層。
* **Premium**: hello Premium 服務層提供可預測的效能，第二個透過第二，每個 Premium 資料庫。 當您選擇 hello Premium 服務層時，您可以調整大小根據 hello 尖峰負載，該資料庫的資料庫應用程式。 hello 計劃移除的案例中的效能變動而可能導致小型查詢 tootake 超過預期的延遲的作業。 此模型可大幅簡化 hello 開發和產品驗證程序，針對需要 toomake 尖峰資源需求、 效能變動或查詢延遲相關的強式陳述式應用程式。 大多數進階服務層使用案例具有下列一或多項特性︰
  * **高尖峰負載**。 應用程式需要大量 CPU、 記憶體或輸入/輸出 (I/O) toocomplete 其作業需要專用、 高效能層級。 例如，已知 tooconsume 資料庫作業數個 CPU 核心數相當長的時間是 hello Premium 服務層的候選項目。
  * **許多並行要求**。 某些資料庫應用程式會為許多並行要求提供服務，例如，在為具有高流量的網站提供服務時。 基本和標準服務層限制的每個資料庫的並行要求的 hello 數目。 需要更多連線的應用程式需要 toochoose 適當預留大小 toohandle hello 最大要求數目。
  * **低延遲**。 某些應用程式需要 tooguarantee 回應 hello 資料庫的最少的時間。 特定的預存程序稱為更廣泛的客戶作業的一部分，您可能必須需求 toohave 從該呼叫傳回超過 20 毫秒，99%的 hello 時間。 此類型的應用程式從 hello Premium 服務層的優點，toomake 確定該 hello 必要的運算能力使用。
* **Premium RS**: hello Premium RS 層專為設計，不需要大量 IO 的工作負載 hello 最高的可用性保證。 範例包括高效能工作負載或其中 hello 資料庫不是 hello 系統的記錄分析工作負載測試。

您需要 SQL database 的 hello 服務層級取決於每個資源維度的 hello 尖峰負載需求。 有些應用程式雖使用少量的某一資源，但卻對其他資源有大量需求。

### <a name="service-tier-capabilities-and-limits"></a>服務層的功能和限制

在每個服務層，您可以設定 hello 效能層級，讓您擁有 hello 彈性 toopay 只針對您需要的 hello 容量。 您可以在工作負載變更時向上或向下 [調整容量](sql-database-service-tiers.md)。 例如，如果在 hello 後-學校購物旺季期間，資料庫工作負載很高，您可能會增加 hello hello 資料庫的效能層級設定的時間，7 月到 9。 當旺季結束時，您可以將效能等級降低。 您可以減少您付費最佳化您的業務您雲端環境 toohello 季節分析。 此模型也非常適合軟體產品發行週期。 測試小組可以在執行測試回合時配置容量，然後在測試完成時釋放該容量。 在容量要求模型中，您可以在需要時付費使用容量，避免將支出花費在可能很少使用的專用資源上。

### <a name="why-service-tiers"></a>為何使用服務層？
雖然每個資料庫工作負載各有不同的服務層的 hello 用途是 tooprovide 各種效能層級的效能可預測性。 對資料庫有大規模資源需求的客戶，則可以在更專用的運算環境中工作。

## <a name="tune-your-application"></a>微調應用程式
在傳統的內部部署 SQL Server，hello 的初始容量規劃的程序通常會分開與 hello 的生產環境中執行應用程式的程序。 先購買硬體和產品授權，之後再微調效能。 當您使用 Azure SQL Database 時，就是個不錯的主意 toointerweave hello 處理執行應用程式和微調。 與 hello 隨選容量付費的模型，您可以微調您的應用程式 toouse hello 需要最少資源，而不是過度佈建硬體根據未來的成長計畫應用程式，通常就是不正確的猜測。 有些客戶可能會選擇不 tootune 應用程式，並改為選擇 toooverprovision 硬體資源。 如果您不想 toochange 關鍵應用程式繁忙期間，這種方法可能是不錯的想法。 但是，微調應用程式可以最小化資源需求，並降低每月帳單金額當您使用 Azure SQL Database 中的 hello 服務層。

### <a name="application-characteristics"></a>應用程式特性
雖然 Azure SQL Database 服務層是設計的 tooimprove 效能穩定性和可預測性應用程式，但是一些最佳作法可協助您微調您的應用程式 toobetter 利用 hello 效能層級的資源。 雖然許多應用程式有大幅的效能改善只是藉由切換 tooa 較高的效能層級或服務層，某些應用程式需要其他微調 toobenefit 較高層級的服務。 為了提高效能，請考慮為具有下列特性的應用程式進行額外的應用程式微調︰

* **因為「多對話」行為而使效能變慢的應用程式**。 多對話的應用程式進行過多的資料存取作業機密 toonetwork 延遲。 您可能需要 toomodify 這些種類的應用程式 tooreduce hello 資料存取作業 toohello SQL 資料庫數目。 例如，您可能會使用技術如批次處理臨機操作查詢或移動 hello 查詢 toostored 程序來改善應用程式的效能。 如需詳細資訊，請參閱 [批次查詢](#batch-queries)。
* **無法由整部單一電腦支援之具有大量工作負載的資料庫**。 資料庫如果超出最高 Premium 效能層級 hello hello 資源可能受益於向外延展 hello 工作負載。 如需詳細資訊，請參閱[跨資料庫分區化](#cross-database-sharding)和[功能資料分割](#functional-partitioning)。
* **具有次佳查詢的應用程式**。 應用程式，特別是那些在 hello 資料存取層中，有未經適當微調的查詢可能不會受益較高的效能層級。 這包括缺少 WHERE 子句、具有遺漏的索引或具有過時統計資料的查詢。 這些應用程式會受益於標準查詢效能微調技術。 如需詳細資訊，請參閱[遺漏索引](#identifying-and-adding-missing-indexes)和[查詢微調和提示](#query-tuning-and-hinting)。
* **具有次佳資料存取設計的應用程式**。 具有內在資料存取並行問題的應用程式，例如死結，可能無法受益於較高的效能等級。 請考慮減少針對 hello Azure SQL Database 上 hello 用戶端快取資料以 hello Azure 快取服務的來回存取或另一種快取技術。 請參閱 [應用程式層快取](#application-tier-caching)。

## <a name="tune-your-database"></a>微調資料庫
在本節中，我們查看一些技術，您可以使用 tootune Azure SQL Database toogain hello 達到最佳效能，您的應用程式，並執行以 hello 最低效能層級。 其中一些技術符合傳統的 SQL Server 微調最佳做法，但有些則是特定 tooAzure SQL 資料庫。 在某些情況下，您可以檢查資料庫 toofind 區域 toofurther 微調的 hello 耗用資源，並擴充 Azure SQL Database 中的傳統 SQL Server 技術 toowork。

### <a name="identify-performance-issues-using-azure-portal"></a>使用 Azure 入口網站找出效能問題
hello 遵循 hello Azure 入口網站中的工具可協助您分析及修正效能問題與您的 SQL 資料庫：

* [查詢效能深入解析](sql-database-query-performance.md)
* [SQL Database 建議程式](sql-database-advisor.md)

hello Azure 入口網站有這兩種工具的詳細資訊及如何 toouse 它們。 tooefficiently 診斷並更正問題，建議您先嘗試 hello Azure 入口網站中的 hello 工具。 我們建議您使用 hello 手動微調我們將討論接下來，遺漏索引和查詢微調，在特殊情況下的方法。

如需識別 Azure SQL Database 中問題的詳細資訊，可在[效能監視](sql-database-single-database-monitor.md)一文中找到。

### <a name="identifying-and-adding-missing-indexes"></a>找出並新增遺漏的索引
常見的問題，OLTP 資料庫效能的相關 toohello 實體資料庫設計。 資料庫結構描述的設計和轉移通常不會經過大規模測試 (無論是在負載或資料數量)。 不幸的是，hello 效能的查詢計劃可能會接受小的標尺上，但大大降級生產層級的資料磁碟區 之下。 hello 此問題最常見來源是 hello 缺乏適當的索引 toosatisfy 篩選或查詢中的其他限制。 遺漏的索引通常會在索引搜尋可以滿足時，以資料表掃描的形式呈現。

在此範例中，hello 選取的查詢計劃使用掃描時即已足夠搜尋：

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![具有遺漏索引的查詢計劃](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Azure SQL Database 可協助您尋找和修正常見的遺漏索引狀況。 Azure SQL Database 內建的 Dmv 查看所在的索引將大幅降低 hello 估計成本 toorun 查詢的查詢編譯。 執行查詢時，SQL Database 可讓您追蹤每個查詢計劃的執行頻率，並追蹤 hello 預估執行查詢計劃與 hello hello 之間的間距想像一個該索引存在位置。 您可以使用這些 Dmv tooquickly 猜測哪些變更 tooyour 實體資料庫設計可能會改善資料庫和及其真實工作負載的整體工作負載成本。

您可以使用這個查詢 tooevaluate 可能會遺漏索引：

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

在此範例中，hello 查詢導致這項建議：

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

它建立之後，該相同的 SELECT 陳述式會挑選不同的計劃，而不是掃描的速度，會使用搜尋，並接著會更有效率地執行 hello 計劃：

![具有已更正索引的查詢計劃](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

hello 重要深入解析為該 hello 共用 I/O 容量，商品系統限制比專用的伺服器電腦的多。 最小化在 hello DTU hello Azure SQL Database 服務層的每個效能層級的 hello 系統的不必要 I/O tootake 優點最大沒有 premium。 選擇適當的實體資料庫設計可以大幅改善個別查詢的 hello 延遲、 改善並行處理的要求每個延展單位的 hello 輸送量和 hello 成本必要的 toosatisfy hello 查詢降至最低。 如需 hello 遺漏索引 Dmv 的詳細資訊，請參閱[sys.dm_db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx)。

### <a name="query-tuning-and-hinting"></a>查詢微調和提示
Azure SQL Database 中的 hello 查詢最佳化工具是類似 toohello 傳統 SQL Server 查詢最佳化工具。 大部分的 hello 最佳做法可以微調查詢和了解 hello 推理模型限制 hello 查詢最佳化工具也會套用 tooAzure SQL 資料庫。 如果您微調查詢 Azure SQL Database 中的，您可能會收到 hello 減少彙整資源需求的另一個好處。 您的應用程式可能無法 toorun 較低的成本較從未微調的同等項目，因為它可以在較低的效能層級執行。

一般 SQL Server 中，且這也適用於 SQL Database tooAzure 範例是 hello 查詢最佳化工具 「 探查 」 參數的方式。 在編譯期間，hello 查詢最佳化工具會評估 hello 參數 toodetermine 目前值，是否可以產生更接近最佳的查詢計劃。 雖然這個策略通常會導致 tooa 速度明顯比編譯時沒有已知的參數值的計劃的查詢計畫，但目前 ﹐ imperfectly 同時在 SQL Server 和 Azure SQL Database 中。 有時不已探查 hello 參數，以及有時 hello 已探查參數但 hello 產生的計畫為次佳的 hello 組完整的工作負載中的參數值。 Microsoft 包含查詢提示 （指示詞），因此您可以更自覺指定意圖及覆寫參數探查 hello 預設行為。 通常，如果您使用提示時，您可以修正所在 hello 預設 SQL Server 或 Azure SQL Database 行為並不完美對特定客戶工作負載的情況。

hello 下一個範例示範如何 hello 查詢處理器在其中產生次佳的效能和資源需求的計劃。 此範例也會示範如果您使用查詢提示，則可以降低 SQL Database 的查詢執行時間和資源需求︰

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

hello 安裝程式碼會建立具有扭曲資料分佈的資料表。 hello 最佳查詢計劃與已選取哪一個參數為基礎。 不幸的是，hello 計畫快取行為不會永遠重新編譯 hello 查詢是根據 hello 最常用的參數值。 因此，它可能會快取並用於許多值，即使在不同的計劃可能平均是較佳的計劃選擇次佳計畫 toobe。 接著 hello 查詢計畫會建立兩個完全相同，不同之處在於其中一個有特殊的查詢提示的預存程序。

**範例 (第 1 部分)**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**範例 (第 2 部分)**

（我們建議您等待至少 10 分鐘的時間才能開始 hello 範例中，第 2 部分，以便在 hello 所產生的遙測資料截然不同 hello 結果）。

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

此範例中的每個部分嘗試 toorun 參數化的 insert 陳述式 1,000 次 (toogenerate 足夠的負載 toouse 做為測試資料集)。 當它執行預存程序時，hello 查詢處理器會檢查其 （參數 「 探查 」） 的第一次編譯期間所傳入 toohello 程序的 hello 參數值。 hello 處理器快取 hello 產生的計畫，而且會將它用於更新的引動過程，即使 hello 參數值不同。 hello 最佳計劃可能會不能在所有情況下。 有時候您需要 tooguide hello 最佳化工具 toopick hello 平均案例，而不是 hello 特定情況下從第一次編譯 hello 查詢更佳的計劃。 在此範例中，hello 初始計畫會產生 「 掃描 」 計畫，讀取所有資料列 toofind 每個符合 hello 參數的值：

![使用掃描計劃微調查詢](./media/sql-database-performance-guidance/query_tuning_1.png)

因為我們使用 hello 值 1 執行 hello 程序，所以 hello 產生的計畫適合 hello 值 1 但 hello 資料表中的所有其他值的次佳。 hello 結果可能不是您想要一樣 toopick 每個計劃，隨機的因為 hello 計畫執行速度更慢，並使用更多資源。

如果您執行與 hello 測試`SET STATISTICS IO`設定得`ON`，在此範例中的 hello 邏輯掃描工作已完成幕後 hello。 您可以看到有 1,148 讀取 hello 計劃 （這是沒有效率，如果 hello 平均案例是 tooreturn 只有一個資料列） 所完成：

![使用邏輯掃描微調查詢](./media/sql-database-performance-guidance/query_tuning_2.png)

hello 第二個部分的 hello 範例 hello 編譯過程中使用查詢提示 tootell hello 最佳化工具 toouse 特定值。 在此情況下，它會強制 hello 查詢處理器 tooignore hello 傳遞值當做 hello 參數，並改為 tooassume `UNKNOWN`。 這是指具有 hello 資料表 （忽略誤差） 中的 hello 平均頻率的 tooa 值。 hello 產生的計畫是以搜尋為基礎的計畫，比較快，使用較少的資源平均，比 hello 計畫在這個範例的第 1 部分：

![使用查詢提示微調查詢](./media/sql-database-performance-guidance/query_tuning_3.png)

您可以看到在 hello hello 效果**sys.resource_stats**資料表 （沒有從您執行 hello 測試並 hello 資料時於其中填入 hello 資料表 hello 時間延遲）。 此範例中，第 1 部分期間 hello 22:25:00 時段執行和第 2 部分在 22:35:00 執行。 hello 較早的時段使用的資源比 hello （因為計畫效率改善） 更新版本的其中一個該時間視窗中。

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![查詢微調範例結果](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> 雖然在此範例中的 hello 磁碟區是刻意小，hello 的次佳參數的效果可能會顯著，尤其是較大的資料庫。 hello 差異，在極端的情況下，可以在快速的情況下 （秒） 之間的速度慢的情況下的小時。
> 
> 

您可以檢查**sys.resource_stats** toodetermine 是否 hello 測試更多或較少使用的資源使用比其他測試。 當您比較資料時，區隔 hello 計時的測試，讓它們不在 hello hello 在同一個 5 分鐘視窗**sys.resource_stats**檢視。 hello hello 練習的目標是 toominimize hello 的資源總數和不 toominimize hello 尖峰資源。 一般而言，最佳化一段延遲的程式碼也可減少資源耗用量。 請確定 hello 做的變更 tooan 應用程式所需，且 hello 變更不造成負面影響的人可能會在 hello 應用程式中使用查詢提示的 hello 客戶經驗。

通常如果工作負載有一組重複查詢，它會建立有意義 toocapture 並驗證 hello 牽動計畫選擇，因為它在磁碟機 hello 最低資源大小單位必要的 toohost hello 資料庫。 進行驗證後，偶爾重新檢查您要確定它們已不降級 toohelp hello 計劃。 您可以深入了解 [查詢提示 (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx)。

### <a name="cross-database-sharding"></a>跨資料庫分區化
Azure SQL Database 在商用硬體上執行，因為單一資料庫的 hello 容量限制會低於傳統的內部部署 SQL Server 安裝。 Hello 限制 Azure SQL Database 中的單一資料庫內不適合 hello 作業時，有些客戶的使用分區化技術 toospread 資料庫作業的多個資料庫。 在 Azure SQL Database 上使用分區化技術的大部分客戶都會在跨多個資料庫的單一維度上分割其資料。 這個方法時，您需要 toounderstand OLTP 應用程式通常會執行適用於 tooonly 一個資料列或 tooa 小型群組 hello 結構描述中的資料列的交易。

> [!NOTE]
> SQL Database 現在提供程式庫 tooassist 與分區化。 如需詳細資訊，請參閱 [彈性資料庫用戶端程式庫概觀](sql-database-elastic-database-client-library.md)。
> 
> 

例如，如果資料庫有客戶名稱、 訂單及訂單詳細資料 （例如 hello 隨附於 SQL Server 的傳統範例 Northwind 資料庫)，您無法這個資料分割成多個資料庫分組為 hello 與客戶相關的訂單與訂單詳細資料資訊。 您可保證 hello 客戶的資料保持在單一資料庫中。 hello 應用程式會將不同客戶分割到各個資料庫，有效地將 hello 負載分散到多個資料庫。 分區化中，客戶不只可以避免在 hello 最大資料庫大小上限，但 Azure SQL Database 也可以處理的工作負載，會明顯地大於 hello 限制的 hello 不同的效能層級，只要每個個別資料庫符合其DTU。

資料庫分區化不會減少方案的 hello 彙整資源容量，卻是非常有效率地支援非常大型的解決方案，跨多個資料庫。 每個資料庫可以在不同的效能層級 toosupport 非常大，資源需求高的 「 有效 」 資料庫中執行。

### <a name="functional-partitioning"></a>功能資料分割
SQL Server 使用者通常會在單一資料庫內結合許多功能。 例如，如果某個應用程式邏輯 toomanage 商店庫存的該資料庫可能有清查之後，追蹤採購單、 預存程序，以及管理月底的報告的索引或具體化檢視相關聯的邏輯。 這項技術可讓您更輕鬆 tooadminister hello 資料庫作業，像是備份，但它也會跨所有應用程式功能需要您 toosize hello 硬體 toohandle hello 尖峰負載。

如果您使用 Azure SQL Database 中的向外延展架構，它是個不錯的主意 toosplit 的不同功能成不同的資料庫應用程式。 使用這項技術時，每個應用程式都可以獨立縮放。 當應用程式變得忙碌 （並 hello hello 資料庫增加的負載），hello 管理員可以選擇每個函式的獨立的效能層級 hello 應用程式中。 Hello 限制，這種架構，與在應用程式可以是大於單一商用電腦可處理因為 hello 負載分散在多部電腦。

### <a name="batch-queries"></a>批次查詢
對於使用大量的存取資料的應用程式，經常臨機操作查詢，大量的回應時間是花費在 hello 應用程式層與 hello Azure SQL Database 層之間的網路通訊。 即使同時 hello 應用程式和 Azure SQL Database 位於相同的資料中心，hello hello 兩者之間的網路延遲可能會大量的資料存取作業放大的 hello。 round tooreduce hello 網路往返 hello 資料存取作業時，請考慮使用 hello 選項 tooeither 批次 hello 臨機操作查詢或 toocompile 它們做為預存程序。 如果您批次 hello 臨機操作查詢，您可以以單一路線 tooAzure SQL Database 中的一個大型批次傳送多個查詢。 如果您編譯的預存程序中的臨機操作查詢，您無法達到的 hello 如同批次處理它們結果相同。 使用預存程序也可讓您 hello 優點增加快取 hello Azure SQL Database 中的查詢計畫，因此您可以使用 hello hello 機會預存程序一次。

某些應用程式是寫入密集型的。 有時候，您可以考慮 toobatch 如何一起寫入減少 hello 總 I/O 負載的資料庫上。 這通常與在預存程序及特定查詢內使用明確的交易而不是自動認可的交易一樣容易。 如需評估您可以使用的不同技術，請參閱 [Azure 中 SQL Database 應用程式的批次處理技術](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx)。 實驗您自己的工作負載 toofind hello 右模型進行批次處理。 會確定 toounderstand 模型可能會有稍微不同的交易一致性保證。 Hello 適當工作負載，資源使用量降到最低必須尋找 hello 的一致性與效能取捨的正確組合。

### <a name="application-tier-caching"></a>應用程式層快取
某些資料庫應用程式具有大量讀取工作負載。 快取層級可能會降低 hello hello 資料庫上的負載，並使用 Azure SQL Database 可能會降低 hello 效能層級需要的 toosupport 資料庫。 與[Azure Redis 快取](https://azure.microsoft.com/services/cache/)，如果您有大量讀取工作負載時，您可以一次讀取 hello 資料 (或可能是應用程式層電腦，根據設定的方式每一次)，然後將存放在您的 SQL 資料庫以外的該資料。 這是方式 tooreduce 資料庫負載 （CPU 和讀取 I/O），但會影響交易一致性，因為從 hello 快取讀取的 hello 資料可能會與 hello 資料庫中的 hello 資料同步處理。 雖然許多應用程式可接受一定程度的不一致性，但並非所有工作負載都是如此。 您應該充分了解應用程式的任何需求，然後再實作應用程式層快取策略。

## <a name="next-steps"></a>後續步驟
* 如需服務層的詳細資訊，請參閱 [SQL Database 選項和效能](sql-database-service-tiers.md)
* 如需彈性集區的詳細資訊，請參閱[什麼是 Azure 彈性集區？](sql-database-elastic-pool.md)
* 效能和彈性集區的相關資訊，請參閱[時 tooconsider 彈性集區](sql-database-elastic-pool-guidance.md)

