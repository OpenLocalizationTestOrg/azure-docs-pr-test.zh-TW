---
title: "雲端間 aaaQuery 資料庫具有不同的結構描述 |Microsoft 文件"
description: "如何 tooset 垂直分割區的跨資料庫查詢"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>對不同結構描述的雲端資料庫執行查詢 (預覽)
![在不同資料庫中跨資料表查詢][1]

垂直資料分割資料庫使用在不同資料庫的不同資料表集。 這表示該 hello 結構描述是在不同的資料庫不同。 比方說，庫存的所有資料表都位於一個資料庫上，而所有會計相關資料表則位於另一個資料庫上。 

## <a name="prerequisites"></a>必要條件
* hello 使用者必須擁有 ALTER ANY EXTERNAL DATA SOURCE 權限。 此權限會包含 hello ALTER DATABASE 權限。
* ALTER ANY EXTERNAL DATA SOURCE 權限是必要的 toorefer toohello 基礎資料來源。

## <a name="overview"></a>概觀

> [!NOTE]
> 不同於與水平資料分割，這些 DDL 陳述式不相依於定義透過 hello 彈性資料庫用戶端程式庫的分區對應的資料層。
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [建立資料庫範圍認證](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>建立資料庫範圍的主要金鑰和認證
hello 認證會使用 hello 彈性查詢 tooconnect tooyour 遠端資料庫。  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> 請確定該 hello`<username>`不包含任何**"@servername"**後置詞。 
>

## <a name="create-external-data-sources"></a>建立外部資料來源
語法：

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> hello 型別參數必須設定得**RDBMS**。 
>

### <a name="example"></a>範例
hello 下列範例說明如何 hello 使用 hello CREATE 陳述式的外部資料來源。 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

目前的外部資料來源 tooretrieve hello 清單： 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>外部資料表
語法：

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>範例
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

hello 下列範例顯示如何 tooretrieve hello hello 目前資料庫中的外部資料表的清單： 

    select * from sys.external_tables; 

### <a name="remarks"></a>備註
彈性查詢擴充 hello 現有外部資料表語法 toodefine 外部資料表所使用的型別 RDBMS 外部資料來源。 垂直資料分割的外部資料表定義涵蓋 hello 下列層面： 

* **結構描述**: hello 外部資料表 DDL 會定義您的查詢可以使用的結構描述。 提供外部資料表定義中的 hello 結構描述必須 hello hello 實際資料的儲存位置的遠端資料庫中的 hello 資料表 toomatch hello 結構描述。 
* **遠端資料庫參考**: hello 外部資料表 DDL 參考 tooan 外部資料來源。 hello 外部資料來源指定 hello 邏輯伺服器名稱和 hello hello 實際的資料表資料的儲存位置的遠端資料庫的資料庫名稱。 

Hello 上一節中所述，請使用外部資料來源，hello 語法 toocreate 外部資料表如下所示： 

hello DATA_SOURCE 子句會定義用於 hello 外部資料表的 hello 外部資料來源 （也就是 hello 遠端資料庫發生垂直資料分割）。  

hello SCHEMA_NAME 和 OBJECT_NAME 子句 hello 能力 toomap hello 外部資料表定義 tooa 資料表不同的結構描述中 hello 遠端資料庫或使用不同的名稱，tooa 資料表上分別提供。 這是如果您想 toodefine 外部資料表 tooa 目錄檢視或 DMV 遠端的資料庫-或任何其他地方 hello 遠端資料表名稱已被使用在本機的情況下很有用。  

hello 下列 DDL 陳述式從卸除現有的外部資料表定義 hello 本機類別目錄。 它不會影響 hello 遠端資料庫。 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**CREATE/DROP 外部資料表的權限**: ALTER ANY EXTERNAL DATA SOURCE 權限所需的外部資料表 DDL 這也是需要 toorefer toohello 基礎資料來源。  

## <a name="security-considerations"></a>安全性考量
使用者具有存取 toohello 外部資料表會自動存取 toohello 基礎遠端的資料表在 hello hello 外部資料來源定義中提供的認證。 您應謹慎管理順序 tooavoid 討厭的權限提高的權限透過 hello hello 外部資料來源的認證存取 toohello 外部資料表。 規則的 SQL 權限可以在使用的 tooGRANT 或 REVOKE access tooan 外部資料表就如同一般資料表。  

## <a name="example-querying-vertically-partitioned-databases"></a>範例︰查詢垂直資料分割的資料庫
hello 下列查詢會執行三向聯結 hello 兩個區域的資料表訂單和訂單產品線之間 hello 遠端資料表的客戶。 這是 hello 參考資料彈性查詢的使用案例的範例： 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>用於遠端 T-SQL 執行的預存程序：sp\_execute_remote
彈性查詢也會介紹可直接存取 toohello 分區的預存程序。 hello 預存程序稱為[sp\_執行\_遠端](https://msdn.microsoft.com/library/mt703714)而且可以是使用的 tooexecute 遠端預存程序或 hello 遠端資料庫上的 T-SQL 程式碼。 它會採用下列參數的 hello: 

* 資料來源名稱 (nvarchar): hello hello 類型 RDBMS 外部資料來源名稱。 
* 查詢 (nvarchar): hello T-SQL 查詢 toobe 在每個分區上執行。 
* 參數宣告 (nvarchar)-選擇性： hello 查詢參數 （例如 sp_executesql) 中使用的 hello 參數的資料型別定義的字串。 
* 參數值清單 - 選用：以逗號分隔的參數值清單 (如 sp_executesql)。

hello sp\_執行\_遠端使用 hello hello 引動過程參數 tooexecute hello hello 遠端資料庫上給定 T-SQL 陳述式中提供的外部資料來源。 它會使用 hello hello 外部資料來源 tooconnect toohello shardmap manager 資料庫和 hello 遠端資料庫的認證。  

範例： 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a>工具的連線能力
您可以使用一般 SQL Server 連接字串 tooconnect 您 BI 和資料整合工具 toodatabases，已啟用的彈性查詢和定義的外部資料表的 hello SQL 資料庫伺服器上。 請確定 SQL Server 可支援做為您的工具的資料來源。 然後，請參閱 toohello 彈性查詢資料庫與外部資料表就像其他任何 SQL Server 資料庫連線 toowith 工具一樣。 

## <a name="best-practices"></a>最佳作法
* 請確定該 hello 彈性查詢端點的資料庫具有存取 toohello 遠端資料庫，進而存取 Azure 服務在 SQL 資料庫的防火牆設定。 提供在 hello 外部資料來源定義可以成功登入 hello 遠端資料庫，並有 hello 權限 tooaccess hello 遠端資料表，也請確定該 hello 認證。  
* 彈性查詢最適合查詢其中完成大部分的 hello 計算 hello 遠端資料庫上。 通常，您會收到包含選擇性的篩選器述詞可以在 hello 遠端資料庫或可執行 hello 遠端資料庫上的完全聯結評估 hello 最佳查詢效能。 其他的查詢模式可能需要 tooload 大量 hello 遠端資料庫中的資料，以及執行效能很差。 

## <a name="next-steps"></a>後續步驟

* 如需彈性查詢的概觀，請參閱[彈性查詢概觀](sql-database-elastic-query-overview.md)。
* 若要開始撰寫程式碼，請參閱 [開始使用跨資料庫查詢 (垂直資料分割)](sql-database-elastic-query-getting-started-vertical.md)。
* 如需水平資料分割 (分區化) 教學課程，請參閱[開始使用彈性查詢進行水平資料分割 (分區化)](sql-database-elastic-query-getting-started.md)。
* 如需水平資料分割之資料的語法和範例查詢，請參閱[查詢水平資料分割的資料](sql-database-elastic-query-horizontal-partitioning.md)
* 如需會在單一遠端 Azure SQL Database 或一組在水平資料分割配置中作為分區之資料庫上執行 Transact-SQL 陳述式的預存程序，請參閱 [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714)。


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
