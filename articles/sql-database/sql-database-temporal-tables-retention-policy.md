---
title: "aaaManage 歷程記錄中資料的時態表與保留原則 |Microsoft 文件"
description: "深入了解如何 toouse 暫時保留原則 tookeep 歷程記錄資料在您的控制。"
services: sql-database
documentationcenter: 
author: bonova
manager: drasumic
editor: 
ms.assetid: 76cfa06a-e758-453e-942c-9f1ed6a38c2a
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 10/12/2016
ms.author: bonova
ms.openlocfilehash: a72a6111a6cd7322d734d08bf3852e95f5ffea8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-historical-data-in-temporal-tables-with-retention-policy"></a>使用保留原則管理時態表中的歷史資料
時態表會讓資料庫變得更大，特別是當您保留一段很長時間的歷史資料時，而一般資料表還不至於讓資料庫變得這麼大。 因此，歷程記錄資料保留原則，是規劃及管理的每個時態表的 hello 生命週期的重要層面。 Azure SQL Database 中的時態表隨附方便使用的保留機制，可協助您完成這項工作。

時態歷程記錄保留可以在 hello 個別資料表層級，可讓的使用者 toocreate 彈性過時原則設定。 套用暫時保留很簡單： 必須只有一個參數 toobe 資料表建立或結構描述變更期間設定。

定義保留原則之後，Azure SQL Database 會開始定期檢查是否有適合自動清除資料的歷史資料列。 相符的資料列的識別和 hello 歷程記錄資料表中的移除它們發生在 hello 背景工作，排程及執行 hello 系統的透明的方式。 Hello 歷程記錄資料表資料列的存留期條件檢查會根據 hello 資料行來代表 SYSTEM_TIME 週期的結尾。 若保留期限，比方說，設定 toosix 適合清除的資料表資料列數月滿足下列條件的 hello:

````
ValidTo < DATEADD (MONTH, -6, SYSUTCDATETIME())
````

在上述範例中的 hello，我們假設**ValidTo**資料行對應 toohello SYSTEM_TIME 週期的結尾。

## <a name="how-tooconfigure-retention-policy"></a>如何 tooconfigure 保留原則嗎？
設定的時態表的保留原則之前，請先檢查是否已啟用時態歷程記錄保留*hello 資料庫層級*。

````
SELECT is_temporal_history_retention_enabled, name
FROM sys.databases
````

資料庫旗標**is_temporal_history_retention_enabled**組 tooON，根據預設，但使用者可以變更利用 ALTER DATABASE 陳述式。 它也是自動設定 tooOFF 之後[還原時間點](sql-database-recovery-using-backups.md)作業。 tooenable 時態歷程記錄保留為清除，為您的資料庫，執行下列陳述式的 hello:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

> [!IMPORTANT]
> 即使 **is_temporal_history_retention_enabled** 為 OFF，您還是可以設定時態表的保留，但在此情況下，不會觸發自動清除過時的資料列。
> 
> 

在資料表建立期間設定保留原則，藉由指定 hello HISTORY_RETENTION_PERIOD 參數值：

````
CREATE TABLE dbo.WebsiteUserInfo
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH
 (
     SYSTEM_VERSIONING = ON
     (
        HISTORY_TABLE = dbo.WebsiteUserInfoHistory,
        HISTORY_RETENTION_PERIOD = 6 MONTHS
     )
 );
````

Azure SQL Database 可讓您 toospecify 保留期限使用不同的時間單位： 天、 週、 月和年。 如果省略 HISTORY_RETENTION_PERIOD，則假設為 INFINITE 保留。 您也可以明確使用 INFINITE 關鍵字。

在某些情況下，您可以在資料表建立之後 tooconfigure 保留或 toochange 先前設定的值。 在此情況下，請使用 ALTER TABLE 陳述式︰

````
ALTER TABLE dbo.WebsiteUserInfo
SET (SYSTEM_VERSIONING = ON (HISTORY_RETENTION_PERIOD = 9 MONTHS));
````

> [!IMPORTANT]
> 設定 SYSTEM_VERSIONING tooOFF*不會保留*保留週期值。 設定 SYSTEM_VERSIONING tooON HISTORY_RETENTION_PERIOD 沒有明確指定，結果在 hello 無限保留週期。
> 
> 

tooreview 的 hello 保留原則的目前狀態，使用 hello 下列查詢會與針對個別資料表的保留期限的 hello 資料庫層級該聯結暫時保留啟用旗標：

````
SELECT DB.is_temporal_history_retention_enabled,
SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,
T1.name as TemporalTableName,  SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,
T2.name as HistoryTableName,T1.history_retention_period,
T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases
where name = DB_NAME()) AS DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2
````


## <a name="how-sql-database-deletes-aged-rows"></a>SQL Database 如何刪除過時資料列？
hello 清理程序取決於 hello hello 歷程記錄資料表的索引配置。 它是重要的 toonotice，*只有歷程記錄資料表具有叢集索引 （B 型樹狀目錄或資料行存放區） 可以將有限的保留原則設定*。 背景工作會建立所有時態表的 tooperform 過時的資料清理具有有限的保留期限。
清除邏輯 hello 資料列存放區 (b-tree) 的叢集索引刪除過時資料列較小的區塊 （向上 too10K) 最小化資料庫記錄檔和 I/O 子系統的壓力。 雖然將清除邏輯會利用所需的 B 型樹狀目錄索引，刪除早於保留期間無法保證穩固地 hello 資料列的順序。 因此，*上在應用程式中的 hello 清除順序，不接受任何相依性*。

hello hello 叢集資料行存放區的清除工作會移除整個[資料列群組](https://msdn.microsoft.com/library/gg492088.aspx)次 （通常包含 1 百萬個資料列的），這是非常有效率，特別是在高步調產生歷程記錄資料。

![叢集資料行存放區保留](./media/sql-database-temporal-tables-retention-policy/cciretention.png)

當您的工作負載快速產生大量記錄資料時，絕佳的資料壓縮和有效率的保留清除，使得叢集資料行存放區索引成為最佳選擇。 此模式通常用於需要[使用時態表的大量交易處理工作負載](https://msdn.microsoft.com/library/mt631669.aspx)，以追蹤和稽核變更、分析趨勢，或擷取 IoT 資料。

## <a name="index-considerations"></a>索引考量
hello 清除工作資料表與資料列存放區叢集索引需要索引 toostart hello 資料行對應 hello 的結尾，SYSTEM_TIME 週期。 如果沒有這種索引，您就無法設定有限保留期限：

*Msg 13765，層級 16，狀態 1 <br> </br>設定有限的保留期限系統版本設定時態表 'temporalstagetestdb.dbo.WebsiteUserInfo' 上失敗，因為 hello 歷程記錄資料表 'temporalstagetestdb.dbo.WebsiteUserInfoHistory' 不包含必要的叢集的索引。請考慮建立叢集資料行存放區或 B 型樹狀目錄索引開頭 hello 資料行符合結尾 SYSTEM_TIME 期間，hello 歷程記錄資料表上。*

請務必 hello 已經建立 Azure SQL database 的預設歷程記錄資料表的 toonotice 有叢集索引，這是保留原則相容。 如果您嘗試 tooremove 該索引上具有有限的保留週期的資料表時，作業會失敗並 hello 下列錯誤：

*Msg 13766，層級 16，狀態 1 <br> </br>無法卸除叢集的索引 'WebsiteUserInfoHistory.IX_WebsiteUserInfoHistory' hello，因為它用來自動清除過時的資料。如果您需要 toodrop 這個索引，請考慮設定 HISTORY_RETENTION_PERIOD tooINFINITE hello 對應的系統版本設定時態表上。*

Hello 叢集資料行存放區索引上的清除時調如果歷程記錄資料列插入中遞增順序 （依 hello 結束期間資料行的排序），也就是一律 hello 案例專屬的 hello SYSTEM_ 填入 hello 歷程記錄資料表時的 helloVERSIONIOING 機制。 如果 hello 歷程記錄資料表中的資料列不會排序結束期間資料行 （這可能是 hello 情況下，如果您移轉現有的歷程記錄資料），您應該重新建立叢集資料行存放區索引 B 型樹狀目錄正確排序，tooachieve 最佳的資料列存放區索引效能。

避免重建叢集資料行存放區索引上 hello 歷程記錄資料表具有 hello 有限的保留期限，因為它可能會變更 hello 自然 hello 系統版本設定作業所加諸的資料列群組中的順序。 如果您需要 toorebuild hello 歷程記錄資料表上的叢集資料行存放區索引時，執行此動作重建之上相容的 B 型樹狀目錄索引，保留順序 hello 資料列群組所需的一般資料清理。 應該採取相同的方法，如果您使用具有叢集資料行索引，但不保證的資料順序的現有記錄資料表建立時態表的 hello:

````
/*Create B-tree ordered by hello end of period column*/
CREATE CLUSTERED INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory (ValidTo)
WITH (DROP_EXISTING = ON);
GO
/*Re-create clustered columnstore index*/
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory ON WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON);
````

有限的保留期限為 hello 與 hello 叢集資料行存放區索引的歷程記錄資料表設定時，您無法在該資料表上建立額外的非叢集 B 型樹狀目錄索引：

````
CREATE NONCLUSTERED INDEX IX_WebHistNCI ON WebsiteUserInfoHistory ([UserName])
````

上述陳述式嘗試 tooexecute 因下列錯誤 hello:

*訊息 13772，層級 16，狀態 1 <br></br> 無法在時態記錄資料表 'WebsiteUserInfoHistory' 上建立非叢集索引，因為它己定義有限保留期限和叢集資料行存放區索引。*

## <a name="querying-tables-with-retention-policy"></a>使用保留原則來查詢資料表
Hello 時態表上的所有查詢自動都篩選掉比對有限的保留原則，tooavoid 無法預期且不一致的結果，因為 hello 清除 」 工作，可以刪除過時的資料列的歷程記錄資料列*在時間中以及在任何時間點任意順序*。

hello 下圖顯示 hello 簡單查詢的查詢計劃：

````
SELECT * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME ALL;
````

hello 查詢計劃包含額外的篩選套用期間資料行 (ValidTo) 的 tooend hello hello 歷程記錄資料表 （反白顯示） 上叢集索引掃描運算子中。 這個範例假設 WebsiteUserInfo 資料表上已設定一個 MONTH 保留期限。

![保留查詢篩選](./media/sql-database-temporal-tables-retention-policy/queryexecplanwithretention.png)

不過，如果您直接查詢記錄資料表，您可能會看到超過指定保留期限的資料列，但完全不保證會得到重複的查詢結果。 hello 下圖顯示 hello 查詢的查詢執行計劃 hello 歷程記錄資料表上沒有套用其他篩選器：

![在不使用保留篩選的情況下查詢記錄](./media/sql-database-temporal-tables-retention-policy/queryexecplanhistorytable.png)

請勿依賴商務邏輯來讀取超出保留期限的記錄資料表，否則可能會得到不一致或非預期的結果。 建議以 FOR SYSTEM_TIME 子句來使用暫時查詢，以分析時態表中的資料。

## <a name="point-in-time-restore-considerations"></a>還原時間點考量
當您建立新資料庫[還原現有資料庫 tooa 特定點時間](sql-database-recovery-using-backups.md)，它有暫時保留 hello 資料庫層級停用。 (**is_temporal_history_retention_enabled**設定 tooOFF 旗標)。 這項功能可讓您 tooexamine 歷程記錄的所有資料列時還原，而不用過時資料列會先取得 tooquery 移除它們。 您可以使用太*檢查歷程記錄資料超過設定的保留週期*。

假設時態表已指定一個 MONTH 保留期限。 如果您的資料庫高階服務層中建立，您將無法 toocreate 資料庫複本，與總 too35 天，在 hello 過去 hello 資料庫狀態。 這實際上可讓您為向上 too65 天以前的直接查詢 hello 歷程記錄資料表的 tooanalyze 歷程記錄資料列。

如果您想 tooactivate 暫時保留為清除時，執行下列 TRANSACT-SQL 陳述式之後的時間點還原的 hello:

````
ALTER DATABASE <myDB>
SET TEMPORAL_HISTORY_RETENTION  ON
````

## <a name="next-steps"></a>後續步驟
toolearn toouse 時態表，在應用程式中的簽出[開始使用 Azure SQL Database 中的時態表](sql-database-temporal-tables.md)。

請瀏覽 Channel 9 toohear[真實客戶時態實作成功劇本](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions)和監看式[live 時態示範](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016)。

如需有關時態表的詳細資訊，請檢閱 [MSDN 文件](https://msdn.microsoft.com/library/dn935015.aspx)。

