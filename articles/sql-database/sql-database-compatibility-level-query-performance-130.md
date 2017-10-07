---
title: "aaaDatabase 相容性等級 130 的 Azure SQL Database |Microsoft 文件"
description: "在本文中，我們將探索 hello 優勢的相容性層級 130，執行您的 Azure SQL Database 以及運用 hello 優點 hello 新查詢最佳化工具，查詢處理器功能。 我們也會解決 hello 可能副作用 hello hello 現有 SQL 應用程式的查詢效能。"
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>改善 Azure SQL Database 中相容性層級 130 的查詢效能
Azure SQL Database 執行無障礙地數百個資料庫在許多不同的相容性層級，保留，並為所有客戶，以及確保 hello 回溯相容性 toohello 對應版本的 Microsoft SQL Server ！

在本文中，我們將探索 hello 優勢的相容性層級 130，執行您的 Azure SQL Database 以及運用 hello 優點 hello 新查詢最佳化工具，查詢處理器功能。 我們也會解決 hello 可能副作用 hello hello 現有 SQL 應用程式的查詢效能。

歷程記錄的提醒的 SQL 版本 toodefault 相容性層級的 hello 對齊方式如下：

* 100：在 SQL Server 2008 和 Azure SQL Database V11 中。
* 110：在 SQL Server 2012 和 Azure SQL Database V11 中。
* 120：在 SQL Server 2014 和 Azure SQL Database V12 中。
* 130：在 SQL Server 2016 和 Azure SQL Database V12 中。

> [!IMPORTANT]
> 從開始**2016 年 6 月 mid**，在 Azure SQL Database，hello 預設相容性層級會 130 而不是 120 個**新建**資料庫。
> 
> 在 2016 年 6 月中旬前建立的資料庫將「不」  受影響，而且會維持其目前的相容性層級 (100、110 或 120)。 從 Azure SQL Database 版本 V11 tooV12 移轉的資料庫都會有 100 或 110 的相容性層級。 
> 

## <a name="about-compatibility-level-130"></a>關於相容性層級 130
首先，如果您想 tooknow hello 目前相容性層級的資料庫，執行下列 TRANSACT-SQL 陳述式的 hello。

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


在此變更之前就進行 toolevel 130**新**建立資料庫，讓我們檢閱這項變更是所有相關資訊，透過某些非常基本的查詢範例，並請參閱如何的任何人都可以從中受益。

關聯式資料庫中的查詢處理可能會很複雜，而且可能會 toolots 電腦科學和數學 toounderstand hello 固有的設計選項和行為。 本文件中，在 hello 內容已經過刻意簡化的 tooensure 某些最小的技術背景的任何人都可以用來了解 hello 影響 hello 相容性層級變更，並判斷它的優點的應用程式。

讓我們先快速查看哪些 hello 相容性層級 130 會在 [hello] 資料表。  您可以在 [ALTER DATABASE 相容性層級 (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)找到更多詳細資料，但簡短摘要如下︰

* hello Insert select 陳述式的 Insert 作業可以是多執行緒或可以有平行計畫，而這項作業為單一執行緒之前。
* 記憶體最佳化資料表和資料表變數查詢現在可以有平行計劃，而這項作業之前也是單一執行緒作業。
* 記憶體最佳化資料表的統計資料現在可以取樣並會自動更新。 如需詳細資訊，請參閱 [Database Engine 新功能：In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) 。
* 資料行存放區索引的批次模式和資料列模式變更
  * 具有資料行存放區索引的資料表現在會以批次模式排序。
  * 時間範圍彙總現在以批次模式運作，例如 TSQL LAG/LEAD 陳述式。
  * 具有多個不同子句的資料行存放區資料表會以批次模式進行查詢。
  * 在 DOP = 1 之下執行或具有序列計劃的查詢也會以批次模式執行。
* 最後，基數估計的改進實際上相容性層級 120，但如果您執行較低的相容性層級 （也就是 100 或 110）、 hello 移動 toocompatibility 層級 130 也將這些增強功能，以及有這些也可以獲得更佳應用程式的 hello 查詢的效能。

## <a name="practicing-compatibility-level-130"></a>演練相容性層級 130
第一個我們得到一些資料表、 索引和建立隨機資料 toopractice 某些這些新功能。 SQL Server 2016 中，或 Azure SQL Database 下，可以執行 hello TSQL 指令碼範例。 不過，在建立 Azure SQL database 時，請確定您選擇在 hello 最小 P2 資料庫，因為您必須至少有幾個核心 tooallow 多執行緒處理，並因此受益於這些功能。

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


現在，讓我們先尋找 toosome 即將相容性層級 130 的 hello 查詢處理功能。

## <a name="parallel-insert"></a>平行 INSERT
執行下列的 hello TSQL 陳述式執行 hello 相容性層級 120 和 130，它會在單一執行緒模型 (120)，並在多執行緒模型 (130) 中分別執行 hello 插入作業的插入作業。

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


藉由要求 hello hello 實際查詢計劃，查看其圖形表示法或其 XML 內容，您可以判斷哪一個函式會在播放的基數估計。 查看圖 1 中的 hello 計劃-並存，我們可以清楚地看到該 hello 插入的資料行存放區執行會進入從序列中 120 tooparallel 130。 另外請注意顯示兩個平行的箭號，說明現在 hello 迭代器執行的 hello 事實確實平行 hello 130 計劃中的 hello 變更的 hello 迭代器圖示。 如果您有大型的 INSERT 作業 toocomplete，hello 平行執行，連結的 toohello 您有在 hello 資料庫，供您使用的核心數目執行效能。向上 tooa 100 倍視情況 ！

*圖 1： 從相容性層級 130 的序列 tooparallel 插入作業變更。*

![圖 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>序列批次模式
同樣地，當處理資料列的資料移動 toocompatibility 層級 130 啟用批次模式處理。 第一，批次模式作業僅適用於您已備妥資料行存放區索引時。 第二，批次通常代表 ~ 900 個資料列，會使用針對多核心 CPU、 記憶體較高的輸送量最佳化的程式碼邏輯和直接利用 hello hello 盡可能的資料行存放區的壓縮的資料。 在這些情況中下, SQL Server 2016 可以同時發生，處理 ~ 900 的資料列，而不是在 hello 階段 1 個資料列，因此，hello hello 作業的整體額外負荷成本都現在共用 hello 整個批次，減少 hello 整體成本資料列。 此共用的作業基本上與 hello 資料行存放區壓縮結合量可減少選取的批次模式作業中的 hello 延遲。 關於 hello 資料行存放區尋找更多詳細資料和批次模式在[資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)。

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


為顯示下方，觀察 hello 查詢計劃-並存上圖 2 中，我們可以看到到 hello 處理模式已變更 hello 相容性層級，且其結果是，當執行 hello 查詢這兩個相容性層級中，我們可以看到大部分的 hello 處理時間花在資料列模式 （86%) 相較 toohello 批次模式 （14%)、 2 批次已處理的所在。 增加 hello 資料集，hello 權益會逐漸增加。

*圖 2： 從相容性層級 130 的序列 toobatch 模式選取作業的變更。*

![圖 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>排序執行的批次模式
從資料列模式 （相容性層級 120） toobatch 模式 （相容性層級 130） 的類似 toohello 上述項目，但套用的 tooa 排序作業，hello 轉換，改善 hello 效能 hello hello 的排序作業相同的原因。

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


顯示由並行上圖 3，我們可以看到 hello 排序作業，資料列模式代表 81 hello 成本，而 hello 批次模式只代表 19 %hello 成本 （分別 81%和 56 %hello 排序本身上） 的百分比。

*圖 3： 從資料列 toobatch 模式相容性層級 130 排序作業變更。*

![圖 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

很明顯地，這些範例只包含數以萬計的資料列，這會是 nothing 近來查看大多數的 SQL Server 中可用的 hello 資料時。 相反地，只要專案數百萬列的這些，而且這可以轉譯在幾分鐘的時間可以節省運算暫止的工作負載的 hello 本質每天執行。

## <a name="cardinality-estimation-ce-improvements"></a>基數估計 (CE) 改進
使用 SQL Server 2014 引進，可讓任何資料庫相容性層級 120 或更新版本執行 hello 新的基數估計功能使用。 基本上，基數估計是使用 SQL server 將如何執行查詢，根據其估計的成本 toodetermine hello 邏輯。 使用來自該查詢中所涉及的物件相關聯的統計資料的輸入來計算 hello 估計。 實際上，在高層次，基數估計函數以及 hello 值分佈的 hello，相異值計數的相關資訊的資料列計數估計以及重複計數會包含在 hello 資料表和 hello 查詢中參考的物件。 Tooa 選取項目，透過平行序列計畫執行的計劃執行，tooname 一些或取得這些估計不正確，可能會導致 toounnecessary 磁碟 I/O，因為 tooinsufficient 記憶體授權 （也就是 TempDB 溢出）。 結束時，不正確的估計值可能會導致 tooan hello 執行查詢的整體效能降低。 在 hello 其他側邊、 更佳的估計值、 估計較為精確，潛在客戶 toobetter 查詢執行 ！

如前所述，查詢最佳化和評估複雜的主題、 但如果您想 toolearn 更多關於查詢計劃和基數估計工具，您可以參考 toohello 文件[最佳化您的查詢計劃 hello SQL Server 2014基數估計工具](https://msdn.microsoft.com/library/dn673537.aspx)的深入剖析。

## <a name="which-cardinality-estimation-do-you-currently-use"></a>您目前使用哪個基數估計？
toodetermine 下執行查詢的基數估計，我們只使用 hello 查詢範例如下。 請注意，第一個範例會執行在相容性層級 110，意味著 hello 使用 hello 舊的基數估計函式。

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


完成執行之後，請按一下 hello XML 連結，並查看 hello hello 第一個迭代器的屬性，如下所示。 請注意呼叫目前設於 70 CardinalityEstimationModelVersion hello 屬性名稱。 並不表示 hello 資料庫相容性層級設定 （它設定為在上述的 hello TSQL 陳述式中可見的 110 上），toohello SQL Server 7.0 版，但 hello 值 70 只代表 hello 舊版基數估計功能自 SQL 起可用伺服器 7.0、 SQL Server 2014 （隨附於相容性層級為 120） 之前有沒有主要修訂。

*圖 4: hello CardinalityEstimationModelVersion too70 時設定使用相容性層級為 110 或下方。*

![圖 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

或者，您可以變更相容性層級 too130 hello，並使用 LEGACY_CARDINALITY_ESTIMATION 設定 tooON 與 hello 停用 hello 使用新的基數估計函式，hello [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). 這會是完全 hello 與使用基數估計函式觀點來看，從 110 時使用 hello 最新查詢處理相容性層級相同。 這樣做，您就可以受益於 hello 新查詢處理來自 hello 最新相容性層級 （也就是批次模式） 的功能，但仍依賴 hello 舊的基數估計功能，如有必要。

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


只移動 toohello 相容性等級 120 或 130 啟用 hello 新的基數估計功能。 在這種情況下，too120 或下方的 做為可見 130，則會據以設定 hello 預設 CardinalityEstimationModelVersion。

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*圖 5: hello CardinalityEstimationModelVersion too130 時設定使用 130 的相容性層級。*

![圖 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Witnessing hello 基數估計差異
現在，我們先執行稍微複雜查詢涉及 INNER JOIN 使用 WHERE 子句的部分述詞，並讓我們看看 hello 資料列計數估計 hello 舊的基數估計函數從第一次。

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


有效地執行這項查詢會傳回 200,704 資料列，而 hello 與 hello 舊的基數估計功能的資料列估計宣告 194,284 資料列。 很明顯地，如上述，這些資料列計數結果也取決於頻率執行 hello 先前的範例，其中會填入 hello 不斷地在每次執行的範例資料表。 很明顯地，在查詢中的 hello 述詞也會有影響 hello 實際估計除了 hello 資料表形狀、 資料內容，和如何這項資料實際上相互關聯與彼此。

*圖 6: hello 資料列計數估計超出 194,284 或 6000 的資料列從預期的 hello 200,704 資料列。*

![圖 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

在 hello 同樣地，我們現在執行相同查詢搭配新的基數估計功能 hello hello。

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


查看 hello 以下，我們現在看到該 hello 資料列估計為 202,877，或更為接近而且多於 hello 舊的基數估計。

*圖 7: hello 資料列計數估計現在是 202,877，而不是 194,284。*

![圖 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

事實上，hello 結果集是 200,704 的資料列 （但都取決於您未執行頻率的 hello hello 查詢先前的範例，但更重要的是，hello TSQL 使用 hello rand （） 陳述式，因為 hello 傳回的實際值可能與一個執行 toohello 旁邊）。 因此，在此特定範例中，hello 新的基數估計會執行在估計 hello 的資料列數目，因為 202,877 更接近 too200，704，比 194,284 更好 ！ 最後，如果您變更 WHERE 子句述詞 tooequality hello (而非">"執行個體)，這可能會使 hello 評估 hello 舊與新的基數函式之間更不同，視多少相符記錄而定，您可以取得。

很明顯地，在此情況下，與實際計數相差 ~6000 個資料列，在某些情況下並不代表大量資料。 現在，跨數個資料表和更複雜的查詢，轉置的資料列的這個 toomillions 有時候 hello 估計還可以和關閉數百萬個資料列，因此，hello 挑選向上 hello 錯誤執行計畫，或要求記憶體不足，無法授與前置的風險tooTempDB 轉散，並因此多個 I/O，會高出許多。

如果您有機會 hello，練習這項比較最常見的查詢與資料集，並且親自體驗了多少有些 hello 舊和新估計受到影響，而某些可能就會變得關閉 hello 現實情況下，從更多或某些其他人只較接近 toohello 實際資料列計算實際 hello 結果集中傳回。 取決於它的所有查詢、 hello Azure SQL 資料庫特性、 hello 本質和 hello 大小的資料集和 hello 提供其相關的統計資料的 hello 圖形。 如果您剛剛建立您的 Azure SQL Database 執行個體、 hello 查詢最佳化工具會有 toobuild 了解，而不是重複使用的統計資料的 hello 先前查詢所做的重新執行。 因此，hello 估計是非常內容和幾乎特定 tooevery 伺服器和應用程式的情況。 它是在心的重要層面 tookeep ！

## <a name="some-considerations-tootake-into-account"></a>納入考量的一些考量 tootake
雖然大部分的工作負載而獲益 hello 相容性層級 130 採用您的生產環境的 hello 相容性層級之前，您基本上會有 3 個選項：

1. 您將 toocompatibility 層級 130，並查看項目執行的方式。 如果您注意到某些迴歸，您只設定 hello 相容性層級回復 tooits 原始的層級，或保留 130 和只反向 hello 基數估計回復 toohello 舊版模式 （以上所述，這單獨無法解決 hello 問題）。
2. 您藉此徹底測試您現有的應用程式，類似的生產負載、 微調，以及驗證之前進行 tooproduction hello 效能。 若有任何問題，與上述相同可以永遠返回 toohello 原始相容性層級，或直接反向操作 hello 基數估計回復 toohello 傳統模式。
3. 做為最後一個選項，以及 hello 最新的方式 tooaddress 這些問題，是 tooleverage hello 查詢存放區。 這是現今的建議選項！ tooassist hello 分析您的查詢，在相容性層級 120 或下方與 130，不建議您足夠 toouse 查詢存放區。 查詢存放區與 hello 最新版本的 Azure SQL Database V12，而且其設計目的是 toohelp 您的查詢效能的疑難排解。 將為您收集及呈現有關所有查詢的詳細歷程記錄資訊的資料庫的飛行資料記錄器視為 hello 查詢存放區。 這可大幅減少 hello 時間 toodiagnose 簡化效能鑑識調查並解決問題。 如需詳細資訊，請參閱 [查詢存放區︰您的資料庫的飛行資料記錄器](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)。

在高層級，如果您已經有一組資料庫執行相容性層級 120 或以下，且計劃 toomove hello 其中部分 too130，或因為您的工作負載自動佈建的新資料庫將會很快就會由預設 too130 設定，請考慮hello 下列項目：

* 在變更之前 toohello 新相容性層級在生產環境中的，啟用查詢存放區。 您可以使用參照太[變更 hello 資料庫相容性模式並使用 hello 查詢存放區](https://msdn.microsoft.com/library/bb895281.aspx)如需詳細資訊。
* 接著，測試所有重要的工作負載使用具代表性的資料和類似實際執行環境和發生的比較 hello 效能及與查詢存放區所報告的查詢。 如果您遇到某些迴歸，您可以識別 hello 迴歸的查詢以 hello 查詢存放區，並使用 hello 計畫強制執行查詢存放區中的選項 （也稱為計畫釘選）。 在這種情況下，您針對保持 hello 相容性層級 130 並且 hello 先前的查詢計劃為 hello 查詢存放區的建議。
* 如果您想 tooleverage 新特色與功能的 Azure SQL Database （這執行 SQL Server 2016），但是機密 toochanges 由 hello 相容性層級 130 的最後手段，您可以考慮強制 hello 相容性層級備份使用 ALTER DATABASE 陳述式來符合您的工作負載的 toohello 層級。 但首先，注意 hello 查詢存放區方案釘選 選項處於最佳選項，因為未使用 130 基本上保持在 hello 功能層級的較舊的 SQL Server 版本。
* 如果您有跨越多個資料庫的多租用戶應用程式時，可能需要 tooupdate hello 佈建您的資料庫 tooensure 一致的相容性層級的邏輯，所有的資料庫;舊的和新佈建項目。 應用程式工作負載效能可能是有些資料庫執行不同的相容性層級的機密 toohello 事實，因此，可能需要的任何資料庫的相容性層級一致性 tooprovide hello 相同的順序所有跨 hello 面板中遇到 tooyour 客戶。 請注意，它不是託管，它其實取決於您的應用程式如何受到 hello 相容性層級。
* 最後，有關 hello 基數估計一樣 hello 相容性層級，再繼續在生產環境中，變更它，如果您的應用程式受惠建議 tootest hello 新條件 toodetermine 下的您生產工作負載hello 基數估計的改進。

## <a name="conclusion"></a>結論
使用 Azure SQL Database 所有 SQL Server 2016 增強 toobenefit 清楚可以改善查詢執行。 現狀正是如此！ 當然，任何新功能，像是正確評估必須完成的資料庫工作負載運作 hello 最佳 toodetermine hello 確切條件。 經驗顯示，大部分的工作負載所預期的 tooat 至少執行無障礙地相容性等級 130，同時利用新的查詢處理函式和新的基數估計。 所雖如此，實際上，總是會有一些例外狀況，以及執行適當的到期勤加注意的重要評估 toodetermine 多少您可以從這些增強功能獲益。 同樣地，hello 查詢存放區可以是大的幫助，在此情況下這項工作 ！

隨著 SQL Azure 的發展，您可以預期未來 hello 相容性層級 140。 在適當時機，我們會開始談論未來相容性層級 140 的願景，就像我們在此簡短討論相容性層級 130 的願景一樣。

現在，我們不忘記，從 2016 年 6 月開始，Azure SQL Database，將變更 hello 預設相容性層級 120 too130 新建立的資料庫。 請留意！

## <a name="references"></a>參考
* [Database Engine 新功能](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [部落格︰查詢存放區︰您的資料庫的飛行資料記錄器 (Borko Novakovic，2016 年 6 月 8 日)](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [ALTER DATABASE 相容性層級 (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)
* [Azure SQL Database V12 的相容性層級 130](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [最佳化查詢計劃您的 SQL Server 2014 的基數估計工具 hello 與](https://msdn.microsoft.com/library/dn673537.aspx)
* [資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)
* [落格︰改善 Azure SQL Database 中相容性層級 130 的查詢效能 (Alain Lissoir，2016 年 5 月 6 日)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
