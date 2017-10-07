---
title: "aaaAzure SQL Database 彈性的查詢概觀 |Microsoft 文件"
description: "Hello 彈性查詢功能的概觀"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Azure SQL Database 彈性查詢概觀 (預覽)
hello 彈性的查詢功能 （處於預覽階段） 可讓您 toorun 跨越多個資料庫中 Azure SQL Database TRANSACT-SQL 查詢。 可讓您 tooperform 跨資料庫查詢 tooaccess 遠端資料表，以及 tooconnect Microsoft 和協力廠商工具 （Excel、 power Bi、 Tableau 等） tooquery 到具有多個資料庫的資料層。 使用這項功能，您可以擴充 SQL Database 中的查詢 toolarge 資料層，並將商業智慧 (BI) 報表中的 hello 結果視覺化。


## <a name="why-use-elastic-queries"></a>為何使用彈性的查詢？

**Azure SQL Database**

完全在 T-SQL 中跨 Azure SQL Database 執行查詢。 如此即可進行遠端資料庫的唯讀查詢。 這可讓目前內部部署選擇使用三和四部分名稱或連結的伺服器 tooSQL DB 的 SQL Server 客戶 toomigrate 應用程式。

**適用於標準層**

加法 toohello 高階效能層中的 hello 標準效能層上支援彈性查詢。 參閱 hello 下方的預覽限制在較低效能層級的效能限制。

**推入 tooremote 資料庫**

彈性查詢現在可以推送執行的 SQL 參數 toohello 遠端資料庫。

**預存程序執行**

使用 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) 執行遠端預存程序呼叫或遠端函式。

**彈性**

外部資料表，其中彈性查詢現在可以參考以不同的結構描述或資料表名稱 tooremote 資料表。

## <a name="elastic-query-scenarios"></a>彈性查詢案例

hello 目標是 toofacilitate 查詢其中的多個資料庫參與成單一的整體結果的資料列的案例。 hello 查詢是由 hello 使用者或應用程式直接或間接透過工具已連接的 toohello 資料庫。 使用商業 BI 或資料整合工具 (或無法變更的任何應用程式) 建立報告時，這特別有用。 使用彈性的查詢，您可以查詢跨多個資料庫使用中工具，例如 Excel、 power Bi、 Tableau 或 Cognos hello 熟悉 SQL Server 的連線體驗。
彈性的查詢可讓您輕鬆存取 tooan 整個資料庫集合透過 SQL Server Management Studio 或 Visual Studio 中，所發出的查詢，並加速跨資料庫查詢從 Entity Framework 或其他 ORM 環境。 圖 1 顯示的案例，其中的現有雲端應用程式 (使用 hello[彈性資料庫用戶端程式庫](sql-database-elastic-database-client-library.md)) 組建的向外延展資料層，然後彈性的查詢用來跨資料庫報告。

**圖 1** 相應放大的資料層上使用的彈性查詢

![相應放大的資料層上使用的彈性查詢][1]

彈性查詢的客戶案例的下列拓撲 hello 其特性：

* **垂直資料分割-跨資料庫查詢**(拓撲 1): hello 資料會垂直分割的資料層中的資料庫數目之間。 一般而言，不同的資料表集位於不同的資料庫。 這表示該 hello 結構描述是在不同的資料庫不同。 比方說，庫存的所有資料表都位於一個資料庫上，而所有會計相關資料表則位於另一個資料庫上。 利用此拓撲的常見使用案例需要一個跨 tooquery 或 toocompile 報表跨越多個資料庫中的資料表。
* **水平資料分割-分區化**(拓撲 2): 資料水平分割層 toodistribute 在向外延展資料的資料列。 使用這個方法，hello 結構描述等同上所有參與的資料庫。 這個方法也稱為「分區化」。 分區化可執行，並使用 （1) hello 彈性資料庫工具程式庫或 （2） 自行區分化管理。 彈性的查詢會是跨多個分區使用的 tooquery 或編譯的報表。

> [!NOTE]
> 彈性查詢是最適合偶爾 reporting 位置在大部分的 hello 處理 hello 資料層上執行。 對於繁重的報告工作負載或有更多複雜查詢的資料倉儲案例，也請考慮使用 [Azure SQL 資料倉儲](https://azure.microsoft.com/services/sql-data-warehouse/)。
>  

## <a name="vertical-partitioning---cross-database-queries"></a>垂直資料分割 - 跨資料庫查詢

toobegin 撰寫程式碼，請參閱[入門 （垂直資料分割） 的跨資料庫查詢](sql-database-elastic-query-getting-started-vertical.md)。

彈性的查詢可以是使用的 toomake 資料位於 SQL database 提供 tooother SQL 資料庫。 這可以讓任何其他遠端的 SQL 資料庫從一個資料庫 toorefer tootables 的查詢。 hello 第一個步驟是 toodefine 每個遠端資料庫的外部資料來源。 hello 外部資料來源被定義在 hello 要從中 toogain 存取 tootables hello 遠端資料庫上的本機資料庫。 不不需要在 hello 遠端資料庫上的任何變更。 垂直資料分割的典型案例，不同的資料庫具有不同結構描述，彈性查詢可以使用的 tooimplement 常見使用案例，例如存取 tooreference 資料，而且跨資料庫查詢。

> [!IMPORTANT]
> 您必須具備 ALTER ANY EXTERNAL DATA SOURCE 權限。 此權限會包含 hello ALTER DATABASE 權限。 ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。
>

**參考資料**: hello 拓撲用於參考資料管理。 Hello 在圖中，與參考資料的兩個資料表 （T1 和 T2） 會保留在專用的資料庫。 使用彈性的查詢，您現在可以存取資料表 T1 和 T2 從遠端與其他資料庫，hello 圖所示。 如果參考資料表很小或參考資料表的遠端查詢有選擇性述詞，則使用拓撲 1。

**圖 2**垂直資料分割-使用彈性查詢 tooquery 參考資料

![垂直資料分割-使用彈性查詢 tooquery 參考資料][3]

**跨資料庫查詢**：彈性查詢可促成需要跨多個 SQL Database 進行查詢的使用案例。 圖 3 顯示四個不同的資料庫：CRM、庫存、HR 和產品。 其中一個 hello 資料庫中執行的查詢也需要存取 tooone 或所有 hello 其他資料庫。 使用彈性的查詢，您可以設定此情況下您的資料庫上的每個 hello 四個資料庫執行幾個簡單的 DDL 陳述式。 這個單次設定之後，存取 tooa 遠端資料表的很簡單，參照 tooa 本機資料表，從您的 T-SQL 查詢，或從您的 BI 工具。 如果 hello 遠端查詢不會傳回較大的結果，建議使用這種方法。

**圖 3**垂直資料分割-跨不同資料庫使用彈性查詢 tooquery

![垂直資料分割-跨不同資料庫使用彈性查詢 tooquery][4]

hello 下列步驟設定為需要存取 tooa 資料表位於遠端的 SQL 資料庫，以 hello 相同的垂直資料分割案例的彈性資料庫查詢結構描述：

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource (類型為 **RDBMS**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

執行之後 hello DDL 陳述式，您可以存取遠端資料表"mytable"hello，就好像是本機資料表。 Azure SQL Database 會自動開啟連線 toohello 遠端資料庫、 處理您的要求上 hello 遠端資料庫，並傳回 hello 的結果。

## <a name="horizontal-partitioning---sharding"></a>水平資料分割 - 分區化
使用彈性查詢 tooperform 報告工作透過分區化，也就是，以水平方式分割，資料層需要[彈性資料庫分區對應](sql-database-elastic-scale-shard-map-management.md)toorepresent hello 資料庫 hello 資料層。 一般而言，只有單一分區對應用在此案例中，並具有彈性的查詢功能 （前端節點） 的專用的資料庫做為報告查詢 hello 進入點。 此專用的資料庫需要存取 toohello 分區對應。 圖 4 說明此拓撲和 hello 彈性查詢的資料庫和分區對應具有其組態。 hello 資料層中的 hello 資料庫可以是任何 Azure SQL Database 版本或版別。 如需 hello 彈性資料庫用戶端程式庫和建立分區對應的詳細資訊，請參閱[分區對應管理](sql-database-elastic-scale-shard-map-management.md)。

**圖 4** 水平資料分割 - 使用彈性查詢來報告分區化資料層

![水平資料分割 - 使用彈性查詢來報告分區化資料層][5]

> [!NOTE]
> 彈性查詢資料庫 （前端節點） 可以是另一個資料庫，或者它可以是 hello 相同資料庫主機 hello 分區對應。 任何設定的選擇，請確定該資料庫的服務和效能層是夠高 toohandle hello 預期的登入/查詢要求。

hello 下列步驟設定水平資料分割需要的案例資料表的存取 tooa 集位於的彈性資料庫查詢 （通常） 多個遠端 SQL 資料庫：

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* 建立[分區對應](sql-database-elastic-scale-shard-map-management.md)代表您的資料層使用 hello 彈性資料庫用戶端程式庫。   
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource (類型為 **SHARD_MAP_MANAGER**)
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

一旦您已經執行下列步驟，您就可以存取 hello 水平資料分割的資料表"mytable"，就好像是本機資料表。 Azure SQL Database 會自動開啟多個平行連接 toohello 遠端資料庫 hello 資料表實體上的儲存位置、 處理 hello 要求在 hello 遠端資料庫，並傳回 hello 結果。
Hello hello 水平資料分割案例可以在中找到所需的步驟的詳細資訊[水平資料分割的彈性查詢](sql-database-elastic-query-horizontal-partitioning.md)。

toobegin 撰寫程式碼，請參閱[入門水平資料分割 （分區化） 的彈性查詢](sql-database-elastic-query-getting-started.md)。

## <a name="t-sql-querying"></a>T-SQL 查詢
一旦您已經定義外部資料來源和外部資料表，您可以使用一般 SQL Server 連接字串 tooconnect toohello 資料庫定義外部資料表的位置。 您可以再執行 T-SQL 陳述式透過外部資料表在該連接上有 hello 限制如下所述。 您可以在 hello 文件集主題中找到詳細資訊和範例的 T-SQL 查詢[水平資料分割](sql-database-elastic-query-horizontal-partitioning.md)和[垂直資料分割](sql-database-elastic-query-vertical-partitioning.md)。

## <a name="connectivity-for-tools"></a>工具的連線能力
您可以使用一般 SQL Server 連接字串 tooconnect 應用程式和 BI 或資料的整合工具 toodatabases 具有外部資料表。 請確定 SQL Server 可支援做為您的工具的資料來源。 一旦連接之後，請參閱 toohello 彈性查詢資料庫與 hello 外部資料表中該資料庫，就像您會執行任何其他 SQL Server 資料庫與您連接 toowith 工具。

> [!IMPORTANT]
> 目前不支援使用 Azure Active Directory 與彈性查詢進行驗證。
> 
> 

## <a name="cost"></a>成本
彈性查詢包含在 hello 成本的 Azure SQL Database 的資料庫。 請注意，支援您的遠端資料庫的不同資料中心內比 hello 彈性查詢端點的拓撲，但從遠端資料庫的資料輸出會收費 regular [Azure 率](https://azure.microsoft.com/pricing/details/data-transfers/)。

## <a name="preview-limitations"></a>預覽限制
* 執行第一個彈性查詢最多可能需要 tooa hello 標準效能層上幾分鐘的時間。 這次是必要的 tooload hello 彈性查詢功能。載入效能改善以較高的效能層。
* 尚未支援來自 SSMS 或 SSDT 的外部資料來源或外部資料表的指令碼。
* SQL DB 匯入/匯出還不支援外部資料來源和外部資料表。 如果您需要 toouse 匯入/匯出，匯出之前先卸除這些物件，然後匯入之後重新建立它們。
* 彈性查詢時，目前僅支援唯讀存取 tooexternal 資料表。 您可以不過，完整的 T-SQL 功能資料庫上使用 hello hello 外部資料表定義的位置。 這可以是到，例如保存的暫存結果使用，例如，選取 < column_list > 到 < local_table >，或 toodefine hello 彈性查詢資料庫，而是會參照 tooexternal 資料表上預存程序很有用。
* 除了 nvarchar (max) 以外，外部資料表定義不支援 LOB 類型。 因應措施，您可以建立 hello 會轉換為 nvarchar （max） hello LOB 類型的遠端資料庫的檢視、 hello 檢視，而非 hello 基底資料表上定義外部資料表並再將它轉換回原始 LOB 類型 hello 在查詢中。
* 目前不支援外部資料表的資料行統計資料。 資料表統計資料支援，但是需要手動建立 toobe。

## <a name="feedback"></a>意見反應
請您的體驗的意見反應與彈性查詢和我們分享 Disqus 下列 hello MSDN 論壇，或在 Stackoverflow 上。 我們有興趣所有種類的 hello 服務缺失、 見諒 （功能間距） 相關的意見反應。

## <a name="next-steps"></a>後續步驟

* 若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。
* 如需垂直資料分割之資料的語法和範例查詢，請參閱[查詢垂直資料分割的資料](sql-database-elastic-query-vertical-partitioning.md)
* 如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。
* 如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)
* 如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
