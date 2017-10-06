---
title: "aaaAzure SQL 資料庫中記憶體內部技術 |Microsoft 文件"
description: "Azure SQL Database-記憶體中技術大幅改善的交易式 hello 效能和分析工作負載。 深入了解如何 tootake 運用這些技術。"
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>使用 SQL Database 中的記憶體內部技術將效能最佳化

您可以使用 Azure SQL Database 中的記憶體內部技術，以改善各種工作負載的效能︰交易式 (線上交易處理 (OLTP))、分析 (線上分析處理 (OLAP)) 及混合 (混合式交易/分析處理 (HTAP))。 因為 hello 更有效率的查詢和交易處理、 記憶體中技術也有助於您 tooreduce 成本。 您通常不需要 tooupgrade hello 定價層的 hello 資料庫 tooachieve 效能提升。 在某些情況下，您甚至可以降低 hello 定價層，之際，仍然使用中記憶體內部技術的效能改進。

以下是記憶體中 OLTP 如何幫助 toosignificantly 改善效能的兩個範例：

- 使用記憶體中 OLTP[仲裁商務解決方案時發生無法 toodouble 其工作負載改善 70%的 Dtu](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)。
    - DTU 表示「資料庫輸送量單位」，其中包含對資源耗用的測量。
- hello 下列影片示範以範例工作負載的資源耗用量會顯著改善： [Azure SQL Database 視訊 中的記憶體中 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB)。
    - 如需詳細資訊，請參閱 hello 部落格文章：[記憶體中 OLTP 中 Azure SQL Database 部落格文章](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

記憶體中技術 hello Premium 層，包括高階彈性集區中的資料庫中的所有資料庫中可用。

hello 下列影片說明與 Azure SQL Database 中的記憶體中技術的潛在效能提升。 請記住 hello 的效能提高，請參閱一律取決於許多因素，包括 hello 的本質 hello 工作負載和資料，hello 資料庫的存取模式等等。

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Azure SQL Database 具有下列記憶體中技術 hello:

- 「記憶體內部 OLTP」可增加輸送量並減少交易處理的延遲。 受益於記憶體內部 OLTP 的案例包括︰高輸送量的交易處理 (例如股票交易和網路遊戲)、從事件或 IoT 裝置擷取資料、快取、資料載入，以及暫存資料表和資料表變數等案例。
- *叢集資料行存放區索引*減少您的儲存體使用量 （向上 too10 時間），並改善報告和分析查詢的效能。 您可以使用它與事實資料表中您資料超市 toofit 更多的資料在資料庫中並改善效能。 此外，您可以使用歷程記錄資料中操作資料庫 tooarchive 中，而且是無法 tooquery too10 時間更多資料。
- *非叢集資料行存放區索引*HTAP 說明您 toogain 即時深入了解您的企業，透過查詢 hello 操作高度耗費資源的擷取、 轉換和載入 (ETL) 處理程序直接資料庫而不 hello 需要 toorun 等如 hello 資料倉儲 toobe 填入。 非叢集資料行存放區索引會允許分析查詢的速度非常快執行 hello OLTP 資料庫，同時降低 hello hello 作業的工作負載的影響。
- 您也可以讓 hello 組合的記憶體最佳化資料表與資料行存放區索引。 這種組合可讓您 tooperform 的非常快速交易處理，以及太*同時*執行的分析查詢非常快速地在 hello 上相同的資料。

資料行存放區索引和記憶體內部 OLTP hello SQL Server 產品的一部分自以來 2012年和 2014，分別。 Azure SQL Database 和 SQL Server 共用 hello 相同的記憶體中技術的實作。 未來，這些技術的新功能會先在 Azure SQL Database 中推出，然後才在 SQL Server 中推出。

本主題描述記憶體內部 OLTP 和資料行存放區索引的特定 tooAzure SQL Database 的各個部分，並也包含範例：
- 您會看到這些技術的 hello 影響有關儲存體和資料大小限制。
- 您會看到 toomanage hello 的資料庫，使用這些技術 hello 不同定價層之間移動的方式。
- 您會看到兩個範例將示範 hello 使用的記憶體中 OLTP 為 Azure SQL Database 中的資料行存放區索引。

請參閱下列資源，如需詳細資訊的 hello。

深入了解 hello 技術的詳細資訊：

- [記憶體中 OLTP 概觀和使用方式案例](https://msdn.microsoft.com/library/mt774593.aspx)（包括參考 toocustomer 案例研究和啟動資訊 tooget）
- [記憶體內部 OLTP 的文件](http://msdn.microsoft.com/library/dn133186.aspx)
- [資料行存放區索引指南](https://msdn.microsoft.com/library/gg492088.aspx)
- 混合式交易/分析處理 (HTAP)，也稱為[即時作業分析](https://msdn.microsoft.com/library/dn817827.aspx)

在記憶體中 OLTP 的快速入門：[快速入門 1: T-SQL 效能更快的記憶體內部 OLTP 技術](http://msdn.microsoft.com/library/mt694156.aspx)(其他文章 toohelp 快速入門)

深入了解 hello 技術的相關影片：

- [Azure SQL Database 中的記憶體中 OLTP](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) （其中包含示範的效能優勢在於，和步驟 tooreproduce 這些結果自行）
- [記憶體中 OLTP 的影片： 什麼是當/如何 toouse 它](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [資料行存放區索引：記憶體內部分析影片 (來源：Ignite 2016)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>儲存體和資料大小

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>記憶體內部 OLTP 的資料大小和儲存體上限

記憶體內部 OLTP 包含記憶體最佳化資料表，以用來儲存使用者資料。 這些資料表是在記憶體中的必要的 toofit。 由於管理直接在 hello SQL Database 服務中的記憶體時，我們會有配額的使用者資料的 hello 概念。 這個概念是參照的 tooas*記憶體中 OLTP 儲存體*。

每個受支援的獨立資料庫定價層以及每個彈性集區定價層都包含一定數量的記憶體內部 OLTP 儲存體。 Hello 撰寫本文時，會取得 1 gb 的儲存體每個 125 資料庫交易單位 (Dtu) 」 或 「 彈性資料庫交易單位 (Edtu)。

hello [SQL Database 服務層](sql-database-service-tiers.md)發行項的 hello 官方 hello 記憶體內部 OLTP 可用存放裝置，針對每個支援獨立資料庫及定價層的彈性集區清單。

下列項目累計記憶體中 OLTP 儲存體 500mb hello:

- 記憶體最佳化資料表和資料表變數中的作用中使用者資料列。 請注意，舊的資料列版本不會計入 hello cap。
- 記憶體最佳化資料表上的索引。
- ALTER TABLE 作業的作業負荷。

如果您遇到 hello 端點時，收到外的配額錯誤，而且您就不再能夠 tooinsert 或更新的資料。 toomitigate 這個錯誤，刪除資料，或增加 hello 定價層的 hello 資料庫或集區。

如需監視記憶體中 OLTP 儲存體使用量和幾乎叫用 hello 端點時，設定警示的詳細資訊，請參閱[監視記憶體中儲存](sql-database-in-memory-oltp-monitoring.md)。

#### <a name="about-elastic-pools"></a>關於彈性集區

彈性集區，與 hello 記憶體中 OLTP 儲存體共用 hello 集區中的所有資料庫。 因此，在某個資料庫中的 hello 使用量可能會影響其他資料庫。 對此，您可以採取以下兩個對策︰

- 設定最大的 eDTU 資料庫低於 hello 整個 hello 集區的 eDTU 計數。 這個最大值的上限設定 hello 記憶體中 OLTP 儲存體使用率、 hello 集區，對應 toohello eDTU 計數 toohello 大小中任何資料庫中。
- 設定大於 0 的最小 eDTU。 此最小保證 hello 集區中的每個資料庫都有可用的記憶體中 OLTP 儲存對應 toohello hello 總量設定 Min eDTU。

### <a name="data-size-and-storage-for-columnstore-indexes"></a>資料行存放區索引的資料大小和儲存體

資料行存放區索引不是必要的 toofit 在記憶體中。 因此，hello 只有 hello hello 索引大小上限為 hello 整體資料庫大小上限，而其記錄在 hello [SQL Database 服務層](sql-database-service-tiers.md)發行項。

當您使用叢集資料行存放區索引時，會將單欄式壓縮用於 hello 基底資料表儲存體。 此壓縮會大幅降低 hello 使用者資料，這表示您可以在 hello 資料庫容納更多資料的儲存體使用量。 和 hello 壓縮進一步增加了[單欄式封存壓縮](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression)。 hello，可讓您的壓縮量取決於 hello 的 hello 資料性質，但 10 次 hello 壓縮並不罕見。

例如，如果您有大小上限為 1 tb 的資料庫，而且您使用資料行存放區索引達到 10 次 hello 壓縮，您可以納入總計的 10 TB 的使用者資料 hello 資料庫。

當您使用非叢集資料行存放區索引時，hello 基底資料表仍會儲存在 hello 傳統的資料列存放區格式。 因此，hello 存放裝置節省不是與具有叢集資料行存放區索引的大小。 不過，如果您要取代傳統的非叢集索引的數目與單一資料行存放區索引，您仍然可以看到在 hello hello 資料表的儲存體使用量因而節省整體成本。

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>在不同定價層之間移動使用記憶體內部技術的資料庫

絕不會有任何不相容或其他問題時升級 tooa 較高的定價層，例如，從標準 tooPremium。 hello 可用的功能和資源只能增加。

但降級 hello 定價層可以對您的資料庫產生負面影響。 hello 影響時，特別是當您從 Premium tooStandard 降級明顯或基本資料庫包含記憶體中 OLTP 物件。 記憶體最佳化資料表和資料行存放區索引，就無法使用 hello 降級之後 （即使它們保持可見）。 hello 考量同樣適用於您正在降低 hello 定價層的彈性集區，或移動資料庫與記憶體中技術，為標準或基本彈性集區時。

### <a name="in-memory-oltp"></a>記憶體內部 OLTP

*降級 tooBasic/標準*: hello 標準或基本層中的資料庫中不支援記憶體內部 OLTP。 此外，它不可能 toomove 具有任何記憶體中 OLTP 物件 toohello 標準或基本層的資料庫。

降級 tooStandard Basic 方式 hello 資料庫之前，請移除所有記憶體最佳化資料表和資料表類型，以及所有原生編譯的 T-SQL 模組。

沒有程式設計的方式 toounderstand 指定的資料庫是否支援 In-memory OLTP。 您可以執行下列 TRANSACT-SQL 查詢的 hello:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

如果 hello 查詢傳回**1**，記憶體中 OLTP 支援此資料庫中。


*降級 tooa 低 Premium 層*： 記憶體最佳化資料表中的資料必須符合相關以 hello 定價層的 hello 資料庫或 hello 彈性集區中的 hello 記憶體中 OLTP 儲存區中。 如果您嘗試 toolower hello 定價層或移到集區中沒有足夠的可用記憶體中 OLTP 儲存體、 hello 作業 hello 資料庫失敗。

### <a name="columnstore-indexes"></a>資料行存放區索引

*降級 tooBasic 或標準*： 資料行存放區索引支援只在 hello Premium 定價層，而不是在 hello 標準或基本層。 降級您資料庫 tooStandard 或 Basic，您的資料行存放區索引會變成無法使用。 hello 系統會維護您的資料行存放區索引，但是它絕不會運用 hello 索引。 如果您稍後升級後 tooPremium，資料行存放區索引是立即準備 toobe 運用一次。

如果您有**叢集**層降級之後資料行存放區索引 hello 整份資料表變成無法使用。 因此我們建議您卸除所有*叢集*降級下方 hello Premium 層資料庫之前，資料行存放區索引。

*降級 tooa 低 Premium 層*: hello 整個資料庫都符合內 hello 的資料庫大小上限 hello 目標定價層，或 hello hello 彈性集區中的可用儲存區中此降級會成功。 沒有特定的 hello 資料行存放區索引影響。


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1.安裝 hello 記憶體中 OLTP 範例

您可以建立 hello 有提供 AdventureWorksLT 範例資料庫中 hello 按幾下[Azure 入口網站](https://portal.azure.com/)。 然後，hello 本節中的步驟說明如何擴充 AdventureWorksLT 資料庫使用記憶體中 OLTP 物件，並示範效能優勢。

如需更簡單、但更美觀的記憶體內部 OLTP 效能示範，請參閱︰

- 版本︰[in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- 原始程式碼︰[in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>安裝步驟

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，在伺服器上建立高階資料庫。 設定 hello**來源**toohello 有提供 AdventureWorksLT 範例資料庫。 如需詳細指示，請參閱[建立您的第一個 Azure SQL Database](sql-database-get-started-portal.md)。

2. 使用 SQL Server Management Studio 連接 toohello 資料庫[(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx)。

3. 複製 hello[記憶體中 OLTP TRANSACT-SQL 指令碼](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql)tooyour 剪貼簿。 hello T-SQL 指令碼會建立 hello 必要記憶體中物件在您在步驟 1 中建立的 hello 有提供 AdventureWorksLT 範例資料庫中。

4. Hello T-SQL 指令碼貼到 SSMS 中，然後執行 hello 指令碼。 hello`MEMORY_OPTIMIZED = ON`子句的 CREATE TABLE 陳述式很重要。 例如：


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>錯誤 40536


如果您執行 hello T-SQL 指令碼時，您會收到錯誤 40536，，執行下列 T-SQL 指令碼 tooverify hello 指出資料庫是否支援記憶體中的 hello:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


結果為 **0** 表示不支援 In-Memory，而 **1** 表示提供支援。 toodiagnose hello 問題，請確定該 hello 資料庫位於 hello Premium 服務層。


#### <a name="about-hello-created-memory-optimized-items"></a>關於 hello 建立記憶體最佳化的項目

**資料表**: hello 範例包含下列記憶體最佳化資料表的 hello:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


您可以檢查記憶體最佳化資料表透過 hello**物件總管 中**在 SSMS 中。 以滑鼠右鍵按一下 [資料表] > [篩選] > [篩選設定] > [記憶體已最佳化嗎]。 hello 值等於 1。


或者，您也可以查詢 hello 目錄檢視，例如：


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**原生編譯的預存程序**：您可以透過目錄檢視查詢來檢查 SalesLT.usp_InsertSalesOrder_inmem：


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>執行 hello 範例 OLTP 工作負載

hello 差異 hello 下列兩個*預存程序*hello 第一個程序會使用記憶體最佳化版本的 hello 資料表，在 hello 第二個程序使用 hello 一般磁碟上的資料表：

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


在本節中，您會看到如何 toouse hello 方便**ostress.exe**公用程式 tooexecute hello 壓力層級的兩個預存程序。 您可以比較的兩個 hello 壓力執行 toofinish 需要多久。


當您執行 ostress.exe 時，我們建議您傳遞的 hello 下列兩個設計的參數值：

- 使用 -n100 來執行大量的並行連線。
- 使用 -r500 讓每個連線執行幾百次迴圈。


不過，您可能想 toostart 類似-n10 和 r50 一切運作的 tooensure 較小的值。


### <a name="script-for-ostressexe"></a>Ostress.exe 的指令碼


此區段會顯示為內嵌在我們 ostress.exe 命令列中的 hello T-SQL 指令碼。 hello 指令碼會使用所建立的 hello 您先前安裝的 T-SQL 指令碼的項目。


hello 下列指令碼將具有五個明細項目範例銷售訂單插入記憶體最佳化的 hello 下列*資料表*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


toomake hello *_ondisk*版本 hello ostress.exe 前述 T-SQL 指令碼，您必須取代出現 hello 的兩個*_inmem*與子字串*_ondisk*。 這些取代會影響 hello 資料表和預存程序的名稱。


### <a name="install-rml-utilities-and-ostress"></a>安裝 RML 公用程式和 ostress


在理想情況下，您應該規劃 toorun ostress.exe Azure 的虛擬機器 (VM) 上。 您可以建立[Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) hello 中有提供 AdventureWorksLT 資料庫所在的相同 Azure 的地理區域。 但是您可以改在您的膝上型電腦上執行 ostress.exe。


Hello VM，或您裝載任何選擇，請安裝 hello Replay 標記語言 (RML) 公用程式。 hello 公用程式包括 ostress.exe。

如需詳細資訊，請參閱：
- hello ostress.exe 討論[記憶體中 OLTP 的範例資料庫](http://msdn.microsoft.com/library/mt465764.aspx)。
- [記憶體內部 OLTP 的範例資料庫](http://msdn.microsoft.com/library/mt465764.aspx)。
- hello[部落格安裝 ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)。



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>執行 hello *_inmem*先壓力工作負載


您可以使用*RML cmd 命令提示字元*視窗 toorun 我們 ostress.exe 命令列。 hello 命令列參數會直接以 ostress:

- 同時執行 100 個連線 (-n100)。
- 有 50 次執行 hello T-SQL 指令碼的每個連接 (-r50)。


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


toorun hello 前面 ostress.exe 命令列：


1. 執行下列命令，在 SSMS 中，toodelete hello 已插入的任何先前執行的所有 hello 資料重設 hello 資料庫資料內容：

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. 複製 hello 前面 ostress.exe 命令列 tooyour 剪貼簿的 hello 的文字。

3. 取代 hello `<placeholders>` hello 參數-S-U-P-d 與 hello 更正實際值。

4. 在 [RML 命令] 視窗中執行已編輯的命令列。


#### <a name="result-is-a-duration"></a>結果是持續時間


Ostress.exe 完成時，它會寫入 hello 做為其最後一行 hello RML Cmd 視窗中輸出的執行持續期間。 例如，較短的測試回合持續大約 1.5 分鐘：

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>重設，針對 _ondisk 編輯，然後重新執行


您擁有 hello hello 結果之後*_inmem*執行，請執行下列步驟 hello *_ondisk*執行：


1. 執行下列命令，在 SSMS toodelete hello hello 先前執行所插入的所有 hello 資料重設 hello 資料庫：
```
EXECUTE Demo.usp_DemoReset;
```

2. 編輯 hello ostress.exe 命令列 tooreplace 所有*_inmem*與*_ondisk*。

3. 重新執行 ostress.exe hello，第二次，並擷取 hello 持續時間結果。

4. 同樣地，重設 hello 資料庫 （適用於以負責的態度刪除項目可以大量的測試資料）。


#### <a name="expected-comparison-results"></a>預期的比較結果

我們的測試中記憶體中顯示的效能改善的**9 次**對於這個簡單的工作負載，使用 ostress 在 Azure VM 上執行 hello 相同 Azure 區域為 hello 資料庫。

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2.安裝 hello 記憶體中分析範例


在本節中，您比較 hello IO 和統計資料的結果時使用的傳統 b 型樹狀目錄索引與資料行存放區索引。


針對 OLTP 工作負載進行即時分析，它是通常是最佳 toouse 非叢集資料行存放區索引。 如需詳細資訊，請參閱[已描述的資料行存放區索引](http://msdn.microsoft.com/library/gg492088.aspx)。



### <a name="prepare-hello-columnstore-analytics-test"></a>準備 hello 資料行存放區分析測試


1. 使用 hello Azure 入口網站 toocreate hello 範例從全新的 AdventureWorksLT 資料庫。
 - 使用相同的名稱。
 - 選擇任何進階服務層。

2. 複製 hello [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour 剪貼簿。
 - hello T-SQL 指令碼會建立 hello 必要記憶體中物件在您在步驟 1 中建立的 hello 有提供 AdventureWorksLT 範例資料庫中。
 - hello 指令碼會建立 hello 維度資料表與兩個事實資料表。 hello 事實資料表會填入 3.5 百萬個資料列。
 - hello 指令碼可能需要 15 分鐘 toocomplete。

3. Hello T-SQL 指令碼貼到 SSMS 中，然後執行 hello 指令碼。 hello**資料行存放區**關鍵字 hello **CREATE INDEX**陳述式中非常重要，做為：<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. 將有提供 AdventureWorksLT toocompatibility 層級 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    層級 130 不直接相關的 tooIn 記憶體內部功能。 但層級 130 通常會提供比層級 120 更快的查詢效能。


#### <a name="key-tables-and-columnstore-indexes"></a>重要資料表和資料行存放區索引


- dbo。FactResellerSalesXL_CCI 是具有叢集資料行存放區索引，提供進階 hello 在壓縮的資料表*資料*層級。

- dbo。FactResellerSalesXL_PageCompressed 是一份含有對等一般叢集的索引，以便壓縮只能在 hello*頁面*層級。


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>索引鍵查詢 toocompare hello 資料行存放區索引


有[數個您可以執行的 T-SQL 查詢類型](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql)toosee 效能改進。 在步驟 2 中 hello T-SQL 指令碼，特別注意 toothis 組的查詢。 其中的不同之處只有一行：


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


非叢集資料行存放區索引是在 hello FactResellerSalesXL\_CCI 資料表。

hello 下列 T-SQL 指令碼摘錄列印統計資料 IO 和每個資料表的 hello 查詢的時間。


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

在資料庫中的 hello P2 定價層，您可以利用 hello 叢集資料行存放區索引與 hello 傳統索引相較預期大約 9 次 hello 的效能提高，此查詢。 與 P15，您可以利用 hello 資料行存放區索引預期大約 57 次 hello 效能改善。



## <a name="next-steps"></a>後續步驟

- [快速入門 1：可讓 Transact-SQL 擁有更快效能的記憶體內部 OLTP 技術](http://msdn.microsoft.com/library/mt694156.aspx)

- [在現有的 Azure SQL 應用程式中使用記憶體內部 OLTP](sql-database-in-memory-oltp-migration.md)

- 針對記憶體內部 OLAP [監視記憶體內部 OLTP 儲存體](sql-database-in-memory-oltp-monitoring.md)


## <a name="additional-resources"></a>其他資源

#### <a name="deeper-information"></a>更深入的資訊

- [了解仲裁如何透過 SQL Database 中的記憶體內部 OLTP，讓重要資料庫的工作負載加倍，同時降低 70% 的 DTU](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [Azure SQL Database 中的記憶體內部 OLTP 部落格文章](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [了解記憶體內部 OLTP](http://msdn.microsoft.com/library/dn133186.aspx)

- [了解資料行存放區索引](https://msdn.microsoft.com/library/gg492088.aspx)

- [了解即時作業分析](http://msdn.microsoft.com/library/dn817827.aspx)

- 請參閱[一般工作負載模式和移轉考量](http://msdn.microsoft.com/library/dn673538.aspx) (其中描述記憶體內部 OLTP 經常提供顯著效能改善的工作負載模式)

#### <a name="application-design"></a>應用程式設計

- [記憶體內部 OLTP (記憶體內部最佳化)](http://msdn.microsoft.com/library/dn133186.aspx)

- [在現有的 Azure SQL 應用程式中使用記憶體內部 OLTP](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>工具

- [Azure 入口網站](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
