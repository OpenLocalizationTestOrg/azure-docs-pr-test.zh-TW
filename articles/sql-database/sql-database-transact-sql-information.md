---
title: "aaaResolving T-SQL 差異移轉 Azure SQL 資料庫 |Microsoft 文件"
description: "在 Azure SQL Database 中未完整支援 Transact-SQL 陳述式"
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>移轉 tooSQL 資料庫期間解析 TRANSACT-SQL 的差異   
當[將資料庫移轉](sql-database-cloud-migrate.md)從 SQL Server tooAzure SQL Server，您可能會發現您的資料庫需要的 hello 可移轉 SQL Server 之前某些重新設計。 本主題提供您在執行重新設計和了解為什麼基礎原因 hello hello 重新設計指引 tooassist 是必要的。 toodetect 不相容，使用 hello[資料移轉小幫手 (DMA)](https://www.microsoft.com/download/details.aspx?id=53595)。

## <a name="overview"></a>概觀
Microsoft SQL Server 和 Azure SQL Database 都支援應用程式使用的大部分 Transact-SQL 功能。 例如，hello 核心 SQL 元件，例如資料類型、 運算子、 字串、 算術、 邏輯和資料指標函數，適用於相同 SQL Server 和 SQL Database。 不過，DDL (資料定義語言) 和 DML (資料操作語言) 元素中有幾個 T-SQL 差異導致對 T-SQL 陳述式和查詢僅提供部分支援 (將在本主題中稍後探討)。

此外，有一些功能，而且因為不支援在所有 Azure SQL Database 的語法而設計的相依性 hello master 資料庫和 hello 作業系統 tooisolate 功能。 因此，大多數伺服器層級活動都不適用於 SQL Database。 如果它們設定伺服器層級選項、作業系統元件或指定檔案系統組態，便無法使用 T-SQL 陳述式和選項。 當需要這類功能時，通常會從 SQL Database 或從另一個 Azure 功能或服務以其他方式提供適合的替代方案。 

例如，高可用性會內建 Azure 中，因此 Alwayson 設定不需要 （雖然您可以更快速的復原，萬一嚴重損壞 hello tooconfigure 作用中地理複寫）。 因此，T-SQL 陳述式相關 tooavailability 群組不支援的 SQL 資料庫，並在的 hello 動態管理檢視相關的 tooAlways 也不支援。

如需公司支援以及不支援的 SQL database hello 功能的清單，請參閱[Azure SQL Database 的功能比較](sql-database-features.md)。 hello 這個頁面清單補充的指導方針和功能的主題，並著重在 TRANSACT-SQL 陳述式。

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>具有部分差異的 Transact-SQL 語法陳述式
hello 核心 DDL （資料定義語言） 陳述式可供使用，但某些 DDL 陳述式有擴充功能相關的 toodisk 放置和不支援的功能。 

- CREATE 和 ALTER DATABASE 陳述式有超過三十多個選項。 hello 陳述式包含檔案位置、 FILESTREAM、 和 service broker 選項只會套用 tooSQL 伺服器。 這可能無關緊要如果您建立資料庫之前，您將移轉，但如果您要移轉會建立資料庫的 T-SQL 程式碼應該比較[CREATE DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) hello SQL Server 語法在[建立資料庫 (SQL Server TRANSACT-SQL&AMP;)](https://msdn.microsoft.com/library/ms176061.aspx) toomake 確定支援您使用的所有 hello 選項。 建立 Azure SQL Database 的資料庫也會有服務目標和套用 tooSQL 資料庫的彈性延展選項。
- hello CREATE 和 ALTER TABLE 陳述式具有無法在 SQL Database 使用，因為不支援 FILESTREAM 的 FileTable 選項。
- CREATE 和 ALTER login 陳述式支援，但是 SQL Database 不提供所有 hello 選項。 您的資料庫更容易移植，SQL Database 鼓勵使用的 toomake 自主資料庫使用者，而不是盡可能登入。 如需詳細資訊，請參閱 [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) 及[控制和授與資料庫存取權](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins)。

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>在 SQL Database 中不支援的 Transact-SQL 語法   
TooTransact SQL 陳述式相關的 toohello 不支援的功能中所述此外[Azure SQL Database 的功能比較](sql-database-features.md)hello 下列陳述式和陳述式的群組，不支援。 因此，如果資料庫 toobe 移轉為使用 hello 下列任何一項功能，重新設計您的 T-SQL tooeliminate 這些 T-SQL 功能和陳述式。

- 系統物件的定序
- 相關連接：端點陳述式、`ORIGINAL_DB_NAME`。 SQL Database 不支援 Windows 驗證，但可支援 hello 類似的 Azure Active Directory 驗證。 部分驗證類型需要 hello 最新版本的 SSMS。 如需詳細資訊，請參閱[連接 tooSQL 資料庫或 SQL 資料倉儲使用 Azure Active Directory 驗證](sql-database-aad-authentication.md)。
- 使用三個或四個組件名稱跨資料庫查詢。 (使用[彈性資料庫查詢](sql-database-elastic-query-overview.md)支援跨資料庫唯讀查詢。)
- 跨資料庫擁有權鏈結，`TRUSTWORTHY` 設定
- `DATABASEPROPERTY` 請改用 `DATABASEPROPERTYEX`。
- `EXECUTE AS LOGIN` 請改用 'EXECUTE AS USER'。
- 除了可延伸金鑰管理之外還支援加密
- 事件服務：事件、事件通知、查詢通知
- 檔案位置： 語法相關 toodatabase 檔案位置、 大小和自動受 Microsoft Azure 的資料庫檔案。
- 高可用性： 語法相關 toohigh 可用性透過 Microsoft Azure 帳戶管理。 這包括備份、還原、永遠開啟、資料庫鏡像、記錄傳送、修復模式的語法。
- 記錄讀取器： 依賴 hello 記錄讀取器，這並不適用於 SQL Database 的語法： 推入複寫、 異動資料擷取。 SQL Database 可以是推送複寫文章的訂閱者。
- 函式：`fn_get_sql`、`fn_virtualfilestats`、`fn_virtualservernodes`
- 全域暫存資料表
- 硬體： 語法相關 toohardware 相關伺服器設定： 例如記憶體、 背景工作執行緒、 CPU 相似性，追蹤旗標。 改用服務層級。
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`、`OPENROWSET`、`OPENDATASOURCE` 和四部分的名稱
- .NET Framework：與 SQL Server 整合的 CLR
- 語意搜尋
- 伺服器認證：請改用[資料庫範圍認證](https://msdn.microsoft.com/library/mt270260.aspx)。
- 伺服器層級項目︰伺服器角色、`IS_SRVROLEMEMBER`、`sys.login_token`。 雖然某些伺服器層級權限已由資料庫層級權限取代，但是無法使用伺服器層級權限的 `GRANT`、`REVOKE` 和 `DENY`。 一些有用的伺服器層級 DMV 有相同的資料庫層級 DMV。
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- `sp_configure` 選項和 `RECONFIGURE`。 有些選項可透過 [變更資料庫範圍組態](https://msdn.microsoft.com/library/mt629158.aspx)來使用。
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL Server 代理程式： 依賴 hello SQL Server Agent 或 hello MSDB 資料庫語法： 警示、 運算子、 中央管理伺服器。 改用指令碼，例如 Azure PowerShell。
- SQL Server Audit：請改用 SQL Database 稽核。
- SQL Server 追蹤
- 追蹤旗標： 項目已經被某些追蹤旗標移 toocompatibility 模式。
- Transact-SQL 偵錯
- 觸發程序：伺服器範圍或登入觸發程序
- `USE`陳述式： toochange hello 資料庫內容 tooa 不同的資料庫，您必須建立新的連接 toohello 新資料庫。

## <a name="full-transact-sql-reference"></a>完整 Transact-SQL 參考
如需 Transact-SQL 文法、使用方式和範例的詳細資訊，請參閱《SQL Server 線上叢書》中的＜ [Transact-SQL 參考 (資料庫引擎)](https://msdn.microsoft.com/library/bb510741.aspx) ＞。 

### <a name="about-hello-applies-to-tags"></a>關於 hello"適用於 」 標記
hello TRANSACT-SQL 參考包括主題相關的 tooSQL 伺服器版本 2008 toohello 存在。 Hello 主題標題下方沒有圖示列、 清單 hello 四個 SQL Server 平台，並指出適用性。 例如，可用性群組是在 SQL Server 2012 中導入。 [建立可用性群組](https://msdn.microsoft.com/library/ff878399.aspx)主題指出 hello 陳述式，適用於**（從 2012年起） 的 SQL Server**。 tooSQL Server 2008、 SQL Server 2008 R2、 Azure SQL Database、 Azure SQL 資料倉儲或平行處理資料倉儲，則不適用 hello 陳述式。

在某些情況下，hello 一般主題主旨可用於產品，但有次要產品之間的差異。 hello 差異也會指出在適當的 hello 主題中的中點。 在某些情況下，hello 一般主題主旨可用於產品，但有次要產品之間的差異。 hello 差異也會指出在適當的 hello 主題中的中點。 例如 hello 建立觸發程序主題會提供 SQL 資料庫中。 但 hello **ALL SERVER**選項的伺服器層級觸發程序，表示伺服器層級觸發程序不能用在 SQL 資料庫。 請改用資料庫層級的觸發程序。

## <a name="next-steps"></a>後續步驟

如需公司支援以及不支援的 SQL database hello 功能的清單，請參閱[Azure SQL Database 的功能比較](sql-database-features.md)。 hello 這個頁面清單補充的指導方針和功能的主題，並著重在 TRANSACT-SQL 陳述式。

