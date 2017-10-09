---
title: "aaaIn 記憶體內部 OLTP 改善 SQL txn 效能 |Microsoft 文件"
description: "採用記憶體內部 OLTP tooimprove 交易式的效能在現有的 SQL 資料庫。"
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>使用記憶體中 OLTP tooimprove SQL Database 中的應用程式效能
[記憶體內部 OLTP](sql-database-in-memory.md)可以是交易處理、 資料擷取和暫時性資料案例中，使用的 tooimprove hello 效能[Premium](sql-database-service-tiers.md) Azure SQL Database，而不會增加 hello 定價層。 

> [!NOTE] 
> [了解仲裁如何透過 SQL Database 讓重要資料庫的工作負載加倍，同時降低 70% 的 DTU](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


請遵循這些步驟 tooadopt 記憶體中 OLTP 中現有的資料庫。

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>步驟 1︰請確定您使用高階資料庫
只有高階資料庫支援記憶體內部 OLTP。 如果 hello 傳回結果為 1，則支援記憶體中 (不是 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* 代表*極端交易處理 (Extreme Transaction Processing)*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>步驟 2： 識別物件 toomigrate tooIn In-memory OLTP
SSMS 包含您可以對具有作用中工作負載的資料庫執行的 [交易效能分析概觀]  報告。 hello 報表會識別資料表和預存程序的移轉候選 tooIn 記憶體內部 OLTP。

在 SSMS 中，toogenerate hello 報表：

* 在 [hello**物件總管] 中**，以滑鼠右鍵按一下資料庫節點。
* 按一下 [報表] > [標準報表] > [交易效能分析概觀]。

如需詳細資訊，請參閱[判斷是否將資料表或預存程序應該匯出 tooIn 記憶體內部 OLTP](http://msdn.microsoft.com/library/dn205133.aspx)。

## <a name="step-3-create-a-comparable-test-database"></a>步驟 3：建立可比較的測試資料庫
假設 hello 報表會指出您的資料庫資料表可從正在獲益的已轉換 tooa 記憶體最佳化資料表。 我們建議您先測試所測試 tooconfirm hello 指示。

您需要實際執行資料庫的測試複本。 hello 測試資料庫都應該在 hello 相同服務與您的生產資料庫層級。

tooease 測試時，會調整您的測試資料庫，如下所示：

1. 使用 SSMS 連接 toohello 測試資料庫。
2. tooavoid 需要 hello WITH (SNAPSHOT) 選項，在查詢中的，將 hello 資料庫選項的設定，如 hello 下列 T-SQL 陳述式中所示：
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>步驟 4：移轉資料表
您必須建立和擴展記憶體最佳化的複製要 tootest 的 hello 資料表。 您可以使用下列其中一種方式加以建立：

* hello 方便在 SSMS 中的記憶體最佳化精靈 」。
* 手動 T-SQL。

#### <a name="memory-optimization-wizard-in-ssms"></a>SSMS 中的記憶體最佳化精靈
toouse 此移轉選項：

1. 使用 SSMS 連接 toohello 測試資料庫。
2. 在 [hello**物件總管] 中**hello 資料表上按一下滑鼠右鍵，然後按**Memory Optimization Advisor**。
   
   * hello**資料表記憶體最佳化 Advisor**精靈隨即顯示。
3. 在 hello 精靈中，按一下 **移轉驗證**(或 hello**下一步**按鈕) toosee 如果 hello 資料表有任何不支援的記憶體最佳化資料表中不支援的功能。 如需詳細資訊，請參閱：
   
   * hello*記憶體最佳化檢查清單*中[Memory Optimization Advisor](http://msdn.microsoft.com/library/dn284308.aspx)。
   * [In-Memory OLTP 不支援的 Transact-SQL 建構](http://msdn.microsoft.com/library/dn246937.aspx)。
   * [移轉 tooIn 記憶體內部 OLTP](http://msdn.microsoft.com/library/dn247639.aspx)。
4. 如果 hello 資料表有不支援的功能，hello advisor 可以為您執行 hello 實際結構描述和資料移轉。

#### <a name="manual-t-sql"></a>手動 T-SQL
toouse 此移轉選項：

1. 使用 SSMS （或類似的公用程式），以連接 tooyour 測試資料庫。
2. 取得 hello 完成 T-SQL 指令碼供您的資料表和其索引。
   
   * 在 SSMS 中，以滑鼠右鍵按一下資料表節點。
   * 按一下 [產生資料表的指令碼為] > [建立] > [新增查詢視窗]。
3. 在 hello 指令碼視窗中，加入 WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE 陳述式。
4. 如果沒有叢集索引，請將它變更 tooNONCLUSTERED。
5. 使用 SP_RENAME 來重新命名 hello 現有的資料表。
6. 執行已編輯的 CREATE TABLE 指令碼，以建立 hello 新記憶體最佳化資料表的副本 hello。
7. 複製 hello tooyour 記憶體最佳化資料表使用 INSERT...選取 * 成：

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>步驟 5 (選擇性)：移轉預存程序
hello 記憶體中的功能也可以修改預存程序來改善效能。

### <a name="considerations-with-natively-compiled-stored-procedures"></a>原生編譯預存程序的考量
原生編譯的預存程序必須有下列選項，在其 T-SQL WITH 子句的 hello:

* NATIVE_COMPILATION
* SCHEMABINDING: hello 預存程序的意義資料表不可具有其資料行的定義會影響 hello 預存程序中，任何方式變更，除非您卸除 hello 預存程序。

原生模組必須使用一個大型 [ATOMIC 區塊](http://msdn.microsoft.com/library/dn452281.aspx) 進行交易管理。 沒有明確 BEGIN TRANSACTION 或 ROLLBACK TRANSACTION 的角色。 如果您的程式碼偵測到商務規則的違規情形，它可能會終止 hello 與不可部分完成的區塊[擲回](http://msdn.microsoft.com/library/ee677615.aspx)陳述式。

### <a name="typical-create-procedure-for-natively-compiled"></a>原生編譯的一般 CREATE PROCEDURE
通常 hello T-SQL toocreate 原生編譯的預存程序是類似 toohello 下列範本：

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Hello TRANSACTION_ISOLATION_LEVEL，快照集是 hello 最常見的值為 hello 原生編譯的預存程序。 不過，子集 hello 其他也支援值：
  
  * REPEATABLE READ
  * SERIALIZABLE
* hello 語言值必須存在於 hello sys.languages 檢視。

### <a name="how-toomigrate-a-stored-procedure"></a>如何 toomigrate 預存程序
hello 移轉步驟如下：

1. 取得 hello CREATE PROCEDURE 指令碼 toohello 一般解譯預存程序。
2. 請重寫其標頭 toomatch hello 先前的範本。
3. 確定 hello 預存程序 T-SQL 程式碼是否使用任何原生編譯的預存程序不支援的功能。 視需要實作因應措施。
   
   * 如需詳細資訊，請參閱 [原生編譯預存程序的移轉問題](http://msdn.microsoft.com/library/dn296678.aspx)。
4. 使用 SP_RENAME 來重新命名 hello 舊的預存程序。 或直接加以捨棄。
5. 執行已編輯的 CREATE PROCEDURE T-SQL 指令碼。

## <a name="step-6-run-your-workload-in-test"></a>步驟 6：在測試環境中執行您的工作負載
您會在您的生產資料庫中執行類似 toohello 工作負載的測試資料庫中執行工作負載。 這應該會顯示 hello hello 記憶體中功能的使用資料表和預存程序來達成的效能改善。

Hello 工作負載的主要屬性如下：

* 並行連線數目。
* 讀取/寫入比率。

tootailor 和執行的 hello 測試工作負載，請考慮使用 hello 方便 ostress.exe 工具中所述[這裡](sql-database-in-memory.md)。

toominimize 網路延遲，hello 中執行測試 hello 資料庫所在的相同 Azure 的地理區域。

## <a name="step-7-post-implementation-monitoring"></a>步驟 7：實作後的監視
監視您在生產環境中的記憶體中實作 hello 效能影響，請考慮：

* [監視記憶體內部儲存體](sql-database-in-memory-oltp-monitoring.md)。
* [使用動態管理檢視監視 Azure SQL Database](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>相關連結
* [記憶體內部 OLTP (記憶體內部最佳化)](http://msdn.microsoft.com/library/dn133186.aspx)
* [簡介 tooNatively 編譯的預存程序](http://msdn.microsoft.com/library/dn133184.aspx)
* [記憶體最佳化建議程式](http://msdn.microsoft.com/library/dn284308.aspx)

