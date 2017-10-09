---
title: "aaaSQL 錯誤碼-資料庫連線錯誤 |Microsoft 文件"
description: "了解 SQL Database 用戶端應用程式的 SQL 錯誤碼，例如常見的資料庫連線錯誤、資料庫副本問題，以及一般錯誤。 "
keywords: "sql error code,access sql,database connection error,sql error codes,sql 錯誤碼,存取 sql,資料庫連線錯誤,sql 錯誤碼"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>SQL Database 用戶端應用程式的 SQL 錯誤碼：資料庫連線錯誤和其他問題
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


本文列出 SQL Database 用戶端應用程式的 SQL 錯誤碼，包括資料庫連線錯誤、暫時性錯誤、資源管理錯誤、資料庫副本問題、彈性集區，以及其他錯誤。 大部分的類別是特定 tooAzure SQL 資料庫，而且也不適 tooMicrosoft SQL Server。

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>資料庫連線錯誤、暫時性錯誤，以及其他暫時的錯誤
hello 表涵蓋連線遺失錯誤，和您的應用程式嘗試 tooaccess SQL Database 時，可能會遇到其他暫時性錯誤 hello SQL 錯誤代碼。 如需入門教學課程 tooconnect tooAzure SQL Database，請參閱[連接 tooAzure SQL Database](sql-database-libraries.md)。

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>最常見的資料庫連線錯誤和暫時性錯誤
hello Azure 基礎結構有 hello 能力 toodynamically hello SQL Database 服務中發生大量的工作負載時，重新設定伺服器。  此動態行為可能會導致您的用戶端程式 toolose 其連線 tooSQL 資料庫。 此類錯誤情況稱為「暫時性錯誤」 。

強烈建議您的用戶端程式具有重試邏輯，使它無法重新建立連線，提供給 hello 暫時性錯誤時間 toocorrect 本身。  我們建議您在您第一次重試前延遲 5 秒鐘。 少於 5 秒的延遲之後重試風險非常龐大的 hello 雲端服務。 每個後續的重試 hello 延遲應該指數成長，向上 tooa 60 秒的最大值。

暫時性失敗錯誤通常是資訊清單做為其中一個用戶端程式中的下列錯誤訊息的 hello:

* 伺服器 &lt;Azure_instance&gt; 上的資料庫 &lt;db_name&gt; 目前無法使用。 請重試稍後 hello 連線。 如果 hello 問題持續發生，請連絡客戶支援並提供他們 hello 工作階段追蹤識別碼&lt;session_id&gt;
* 伺服器 &lt;Azure_instance&gt; 上的資料庫 &lt;db_name&gt; 目前無法使用。 請重試稍後 hello 連線。 如果 hello 問題持續發生，請連絡客戶支援並提供他們 hello 工作階段追蹤識別碼&lt;session_id&gt;。 (Microsoft SQL Server，錯誤：40613)
* Hello 遠端主機已強制關閉現有的連接。
* System.Data.Entity.Core.EntityCommandExecutionException： 執行 hello 命令定義時發生錯誤。 請參閱 hello 內部例外狀況。 ---> System.Data.SqlClient.SqlException: hello server 從接收結果時發生傳輸層級錯誤。 (提供者: 工作階段提供者, 錯誤: 19 - 無法使用實際連線)
* 連線嘗試 tooa 次要資料庫失敗，因為 hello 資料庫處於 reconfguration hello 程序，而且很忙碌 hello 主要資料庫上套用新頁面時的使用中交易的 hello 中間。 

如需重試邏輯的程式碼範例，請參閱：

* [SQL Database 和 SQL Server 的連接庫](sql-database-libraries.md) 
* [動作 toofix 連接錯誤及 SQL Database 中的暫時性錯誤](sql-database-connectivity-issues.md)

討論的 hello*封鎖期間*使用 ADO.NET 的用戶端會提供[SQL Server 連接共用 (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx)。

### <a name="transient-fault-error-codes"></a>暫時性錯誤錯誤碼
hello 下列的錯誤是暫時性的並在應用程式邏輯應該重試 

| 錯誤碼 | 嚴重性 | 說明 |
| ---:| ---:|:--- |
| 4060 |16 |無法開啟資料庫"%.& #x2a; ls"hello 登入所要求。 hello 登入失敗。 |
| 40197 |17 |hello 服務發生處理您的要求時發生錯誤。 請再試一次。 錯誤代碼 %d。<br/><br/>您會收到這個錯誤，當 hello 服務已關閉，因為 toosoftware 或硬體升級、 硬體故障或任何其他容錯移轉問題。 hello 錯誤碼 (%d) 內嵌在錯誤 40197 的 hello 訊息提供 hello 種失敗或發生的容錯移轉的其他資訊。 Hello 錯誤程式碼會內嵌在錯誤 40197 的 hello 訊息的一些範例是包括 40020、 40143、 40166 和 40540。<br/><br/>重新連線 tooyour SQL Database 伺服器會自動連線 tooa 良好的資料庫。 您的應用程式必須攔截錯誤 40197、 記錄 hello 內嵌錯誤碼 (%d) 中進行疑難排解，hello 訊息，然後再次嘗試重新連接 tooSQL 資料庫，直到 hello 資源可供使用，且再次建立您的連線為止。 |
| 40501 |20 |hello 服務目前忙碌中。 在 10 秒後，重試 hello 要求。 事件識別碼：%ls。 程式碼：%d。<br/><br/>注意︰如需詳細資訊，請參閱：<br/>• [Azure SQL Database 資源限制](sql-database-resource-limits.md)。 |
| 40613 |17 |資料庫 '%.&#x2a;ls' (在伺服器 '%.&#x2a;ls' 上) 目前無法使用。 請重試稍後 hello 連線。 如果 hello 問題持續發生，請連絡客戶支援並提供他們 hello 工作階段追蹤識別碼 ' %.& #x2a; ls'。 |
| 49918 |16 |無法處理要求。 沒有足夠的資源 tooprocess 要求。<br/><br/>hello 服務目前忙碌中。 請稍後再試 hello 要求。 |
| 49919 |16 |無法處理建立或更新要求。 訂用帳戶 "%ld" 太多建立或更新作業進行中。<br/><br/>hello 服務正忙於處理多個建立或更新您的訂用帳戶或伺服器的要求。 要求目前已封鎖以求資源最佳化。 查詢 [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) 以查看暫止的作業。 等待直到暫止的建立或更新要求已完成，或刪除您其中一個暫止要求，稍後再重試您的要求。 |
| 49920 |16 |無法處理要求。 訂用帳戶 "%ld" 太多作業進行中。<br/><br/>hello 服務正忙於處理多個要求此訂用帳戶。 要求目前已封鎖以求資源最佳化。 查詢 [sys.dm_operation_status](https://msdn.microsoft.com/library/dn270022.aspx) 以查看作業狀態。 等候直到暫止的要求已完成，或刪除您其中一個暫止要求，稍後再重試您的要求。 |
| 4221 |16 |登入 tooread 次要失敗，因為 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING' toolong 等待時間。 hello 複本不是適用於登入，因為資料列版本已遺失 hello 複本已回收時，所傳遞的交易。 以回復或認可 hello hello 主要複本上的使用中交易，就可以解決 hello 問題。 此條件的項目可以藉由避免 hello 主要上的長寫入交易降到最低。 |

## <a name="database-copy-errors"></a>資料庫複製錯誤
Azure SQL Database 中複製資料庫時，可能會遇到下列錯誤 hello。 如需詳細資訊，請參閱 [複製 Azure SQL Database](sql-database-copy.md)。

| 錯誤碼 | 嚴重性 | 說明 |
| ---:| ---:|:--- |
| 40635 |16 |IP 位址 '%.&#x2a;ls' 的用戶端已暫時停用。 |
| 40637 |16 |建立資料庫副本目前已停用。 |
| 40561 |16 |資料庫複製失敗。 其中一個 hello 來源或目標資料庫不存在。 |
| 40562 |16 |資料庫複製失敗。 已經卸除 hello 來源資料庫。 |
| 40563 |16 |資料庫複製失敗。 已經卸除 hello 目標資料庫。 |
| 40564 |16 |資料庫複製失敗，因為 tooan 內部錯誤。 請卸除目標資料庫並再試一次。 |
| 40565 |16 |資料庫複製失敗。 1 個並行資料庫複製的 hello 允許相同的來源。 請卸除目標資料庫並稍後再試一次。 |
| 40566 |16 |資料庫複製失敗，因為 tooan 內部錯誤。 請卸除目標資料庫並再試一次。 |
| 40567 |16 |資料庫複製失敗，因為 tooan 內部錯誤。 請卸除目標資料庫並再試一次。 |
| 40568 |16 |資料庫複製失敗。 來源資料庫已變成無法使用。 請卸除目標資料庫並再試一次。 |
| 40569 |16 |資料庫複製失敗。 目標資料庫已變成無法使用。 請卸除目標資料庫並再試一次。 |
| 40570 |16 |資料庫複製失敗，因為 tooan 內部錯誤。 請卸除目標資料庫並稍後再試一次。 |
| 40571 |16 |資料庫複製失敗，因為 tooan 內部錯誤。 請卸除目標資料庫並稍後再試一次。 |

## <a name="resource-governance-errors"></a>資源管理錯誤
使用 Azure SQL Database 時過度使用資源所造成下列錯誤 hello。 例如：

* 交易已開啟太長時間。
* 交易持有太多鎖定。
* 應用程式耗用太多記憶體。
* 應用程式耗用太多 `TempDb` 空間。

相關主題：

* 以下可提供更詳細的資訊︰ [Azure SQL Database 資源限制](sql-database-resource-limits.md)

| 錯誤碼 | 嚴重性 | 說明 |
| ---:| ---:|:--- |
| 10928 |20 |資源識別碼：%d。 是 %d hello %s hello 資料庫限制，且已達到。 如需詳細資訊，請參閱 [http://go。microsoft。com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637)。<br/><br/>hello 資源 ID 表示已達到 hello 限制的 hello 資源。 背景工作執行緒 hello 資源識別碼 = 1。 工作階段，hello 資源 ID = 2。<br/><br/>*注意：*如需有關此錯誤以及如何 tooresolve，請參閱：<br/>• [Azure SQL Database 資源限制](sql-database-resource-limits.md)。 |
| 10929 |20 |資源識別碼：%d。 hello %s 最小保證是 %d、 最大限制是 %d 和 hello hello 資料庫目前的使用量為 %d。 不過，hello 伺服器目前是過於忙碌 toosupport 要求大於 %d 此資料庫。 如需詳細資訊，請參閱 [http://go。microsoft。com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637)。 或者，請稍後再試一次。<br/><br/>hello 資源 ID 表示已達到 hello 限制的 hello 資源。 背景工作執行緒 hello 資源識別碼 = 1。 工作階段，hello 資源 ID = 2。<br/><br/>*注意：*如需有關此錯誤以及如何 tooresolve，請參閱：<br/>• [Azure SQL Database 資源限制](sql-database-resource-limits.md)。 |
| 40544 |20 |hello 資料庫已達到大小配額。 資料分割或刪除資料、 卸除索引，或請參閱 hello 文件可能的解決方式。 |
| 40549 |16 |工作階段已終止，因為您有長時間執行的交易。 請嘗試縮短您的交易時間。 |
| 40550 |16 |hello 工作階段已終止，因為它取得太多鎖定。 嘗試在單一交易中讀取或修改較少的資料列。 |
| 40551 |16 |hello 工作階段已終止，因為過多`TEMPDB`使用量。 請嘗試修改您查詢 tooreduce hello 暫存資料表的空間使用量。<br/><br/>*提示：*如果您使用暫存物件時，節省空間 hello `TEMPDB` hello 工作階段不再需要暫存物件卸除資料庫。 |
| 40552 |16 |hello 工作階段已終止，因為它過度使用交易記錄檔空間使用量。 請嘗試在單一交易中修改較少的資料列。<br/><br/>*提示：*如果執行大量插入使用 hello`bcp.exe`公用程式或 hello`System.Data.SqlClient.SqlBulkCopy`類別，請嘗試使用 hello`-b batchsize`或`BatchSize`複製 toohello 伺服器在每一筆交易中的資料列的選項 toolimit hello 數目。 如果您要重建索引以 hello`ALTER INDEX`陳述式，請嘗試使用 hello`REBUILD WITH ONLINE = ON`選項。 |
| 40553 |16 |hello 工作階段已終止，因為它過度使用記憶體。 請嘗試修改查詢 tooprocess 較少的資料列。<br/><br/>*提示：*減少 hello 數量`ORDER BY`和`GROUP BY`TRANSACT-SQL 程式碼中的作業會減少查詢的 hello 記憶體需求。 |

## <a name="elastic-pool-errors"></a>彈性集區錯誤
hello 下列錯誤而相關的 toocreating 使用 Elastics 集區。

| 錯誤號碼 | 錯誤嚴重性 | 錯誤格式 | 錯誤說明 | 錯誤原因 | 錯誤修正動作 |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |hello 彈性集區已達到其儲存限制。 hello hello 彈性集區的儲存體使用量不得超過 (%d) Mb。 |彈性集區空間限制 (MB)。 |在達到 「 hello 彈性集區的 hello 存放限制時，請嘗試 toowrite 資料 tooa 資料庫。 |請考慮增加 hello Dtu hello 彈性集區的盡可能在順序 tooincrease 其儲存限制、 減少 hello hello 彈性集區中的個別資料庫所使用的儲存體或從 hello 彈性集區中移除資料庫。 |
| 10929 |EX_USER |hello %s 最小保證是 %d、 最大限制是 %d 和 hello hello 資料庫目前的使用量為 %d。 不過，hello 伺服器目前是過於忙碌 toosupport 要求大於 %d 此資料庫。 請參閱 [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) 以取得協助。 或者，請稍後再試一次。 |每個資料庫的最小 DTU、每個資料庫的最大 DTU |hello hello 彈性集區嘗試的 tooexceed hello 集區限制中的所有資料庫的並行工作者 （要求） 的總數。 |請考慮增加 hello hello 彈性集區的盡可能在順序 tooincrease Dtu 其背景工作限制，或從 hello 彈性集區中移除資料庫。 |
| 40844 |EX_USER |伺服器 '%ls' 上的資料庫 '%ls' 是彈性集區中的 '%ls' 版資料庫，且無法有連續複製關聯性。 |資料庫名稱、資料庫版本、伺服器名稱 |針對彈性集區中的非高階資料庫發出了 StartDatabaseCopy 命令。 |敬請期待 |
| 40857 |EX_USER |找不到伺服器 '%ls' 的彈性集區，彈性集區名稱: '%ls'。 |伺服器名稱、彈性集區名稱 |指定彈性集區不存在於 hello 指定的伺服器。 |請提供有效的彈性集區名稱。 |
| 40858 |EX_USER |彈性集區 '%ls' 已存在於伺服器 '%ls' 中 |彈性集區名稱、伺服器名稱 |指定彈性集區已經存在於指定的邏輯伺服器 hello。 |請提供新的彈性集區名稱。 |
| 40859 |EX_USER |彈性集區不支援服務層 '%ls'。 |彈性集區服務層 |指定的服務層不支援彈性集區佈建。 |提供 hello 正確版本，或保持服務層空白 toouse hello 預設服務層。 |
| 40860 |EX_USER |彈性集區 '%ls' 和服務目標 '%ls' 的組合無效。 |彈性集區名稱、服務層級目標名稱 |如果服務目標指定為 'ElasticPool'，才能同時指定彈性集區和服務目標。 |請指定正確的彈性集區和服務目標組合。 |
| 40861 |EX_USER |hello 資料庫版本 ' %。*ls' 不可以不同於 hello 彈性集區服務層的 ' %。*ls'。 |資料庫版本、彈性集區服務層 |hello 資料庫版本是 hello 彈性集區服務層不同。 |請不要指定資料庫版本所在不同 hello 彈性集區服務層。  請注意該 hello 資料庫版本不需要指定 toobe。 |
| 40862 |EX_USER |彈性集區名稱必須是指定 hello 彈性集區服務目標時指定。 |None |彈性集區服務目標不是彈性集區的唯一識別依據。 |請如果使用 hello 彈性集區服務目標，指定 hello 彈性集區名稱。 |
| 40864 |EX_USER |hello Dtu hello 彈性集區至少必須為 (%d) 的 Dtu 服務層 ' %.* ls'。 |彈性集區的 DTU 數、彈性集區服務層。 |正在嘗試 tooset hello Dtu hello hello 最小限制以下彈性集區。 |請重試設定 hello 彈性集區 tooat hello dtu 數至少 hello 最小限制。 |
| 40865 |EX_USER |hello 彈性集區的 hello dtu 數不得超過 (%d) 的 Dtu 服務層 ' %.* ls'。 |彈性集區的 DTU 數、彈性集區服務層。 |正在嘗試 tooset hello Dtu hello 彈性集區超過 hello 的最大限制。 |請重試將 hello 彈性集區 toono hello dtu 數設定為大於 hello 最大限制。 |
| 40867 |EX_USER |hello 每個資料庫最大 DTU 數必須是在最少的 (%d) 的服務層 ' %.* ls'。 |每個資料庫的最大 DTU、彈性集區服務層。 |嘗試 tooset hello DTU 數目上限，每個資料庫 hello 下列支援限制。 |請考慮使用支援 hello 想要設定的 hello 彈性集區服務層。 |
| 40868 |EX_USER |hello 每個資料庫最大 DTU 數不得超過 (%d) 的服務層 ' %.* ls'。 |每個資料庫的最大 DTU、彈性集區服務層。 |嘗試 tooset hello 的每個資料庫 hello 超出最大 DTU 支援限制。 |請考慮使用支援 hello 想要設定的 hello 彈性集區服務層。 |
| 40870 |EX_USER |hello 每個資料庫的 DTU 最小值不得超過 (%d) 的服務層 ' %.* ls'。 |每個資料庫的最小 DTU、彈性集區服務層。 |嘗試 tooset hello 的最小 DTU 每個資料庫 hello 超過支援限制。 |請考慮使用支援 hello 想要設定的 hello 彈性集區服務層。 |
| 40873 |EX_USER |hello 資料庫 (%d) 和每個資料庫 (%d) 的最小 DTU 數不得超過 hello 彈性集區 (%d) 的 hello Dtu。 |彈性集區中的資料庫數目、每個資料庫的最小 DTU、彈性集區的 DTU 數。 |正在嘗試 toospecify 最小 DTU 數超過 hello hello 彈性集區的 Dtu 的 hello 彈性集區中的資料庫。 |請考慮增加 hello hello 彈性集區的 Dtu 或減少 hello 的最小 DTU 根據每個資料庫，或減少 hello hello 彈性集區中的資料庫數目。 |
| 40877 |EX_USER |除非不包含任何資料庫，否則無法刪除彈性集區。 |None |hello 彈性集區包含一或多個資料庫，因此無法刪除。 |請移除資料庫從順序 toodelete hello 彈性集區。 |
| 40881 |EX_USER |hello 彈性集區 ' %.* ls' 已達到其資料庫計數的限制。  hello hello 彈性集區的資料庫計數限制不得超過 (%d) 與 (%d) 的 Dtu 彈性集區。 |彈性集區名稱、彈性集區的資料庫計數上限、資源集區的 DTU 數。 |嘗試 toocreate 或加入資料庫 tooelastic 集區時已達到 hello 彈性集區的 hello 資料庫計數限制。 |請考慮增加 hello Dtu hello 彈性集區的盡可能順序 tooincrease 在其資料庫限制，或從 hello 彈性集區中移除資料庫。 |
| 40889 |EX_USER |hello Dtu 或是儲存空間限制 hello 彈性集區 ' %.* ls' 不能降低，因為會對其資料庫無法提供足夠的儲存空間。 |彈性集區名稱。 |正在嘗試 hello 彈性集區下其存放裝置使用量 toodecrease hello 儲存體的限制。 |請考慮縮短 hello 儲存體使用量 hello 彈性集區中的個別資料庫，或移除資料庫從順序 tooreduce 中的 hello 集區的 Dtu 或是儲存體限制。 |
| 40891 |EX_USER |hello 的最小 DTU 根據每個資料庫 (%d) 不能超過 hello 每個資料庫 (%d) 的 DTU 最大值。 |每個資料庫的最小 DTU、每個資料庫的最大 DTU。 |正在嘗試 tooset hello 的最小 DTU 根據每個資料庫高於 hello 的每個資料庫最大 DTU。 |請確定 hello 每個資料庫的 DTU 最小值不能超過 hello 的每個資料庫最大 DTU。 |
| TBD |EX_USER |彈性集區中的個別資料庫的 hello 儲存體大小不能超過 hello 所允許的最大大小 ' %.* ls' 的服務層彈性集區。 |彈性集區服務層 |hello hello 資料庫大小上限超過 hello hello 彈性集區服務層所允許的最大大小。 |請設定 hello hello hello 的 hello hello 彈性集區服務層所允許的最大大小的限制範圍內的資料庫的大小上限。 |

相關主題：

* [建立彈性集區 (C#)](sql-database-elastic-pool-manage-csharp.md) 
* [管理彈性集區 (C#)](sql-database-elastic-pool-manage-csharp.md)。 
* [建立彈性集區 (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [監視和管理彈性集區 (PowerShell)](sql-database-elastic-pool-manage-powershell.md)。

## <a name="general-errors"></a>一般錯誤
下列錯誤 hello 不屬於任何先前的類別。

| 錯誤碼 | 嚴重性 | 說明 |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin> 不是有效的名稱，因為它包含無效字元。 |
| 18452 |14 |登入失敗。 hello 登入是來自不受信任的網域，不能與 Windows authentication.%。 & #x2a; ls （Windows 登入不支援這個版本的 SQL Server）。 |
| 18456 |14 |使用者登入失敗 ' %.#x2a;ls'.%。 & #x2a ls %.& #x2a; ls (hello 登入失敗的使用者"%.& #x2a; ls"。 hello 密碼變更失敗。 在登入期間變更密碼在這個版本的 SQL Server 中不受支援。) |
| 18470 |14 |使用者 '%.&#x2a;ls' 登入失敗。 原因： hello 帳戶為 disabled.%。 & #x2a; ls |
| 40014 |16 |多個資料庫不能用於在 hello 相同的交易。 |
| 40054 |16 |在這個版本的 SQL Server 中不支援沒有叢集索引的資料表。 建立叢集的索引並再試一次。 |
| 40133 |15 |此作業在這個版本的 SQL Server 中不受支援。 |
| 40506 |16 |指定的 SID 對這個版本的 SQL Server 無效。 |
| 40507 |16 |'%.&#x2a;ls' 無法在這個版本的 SQL Server 中使用參數叫用。 |
| 40508 |16 |USE 陳述式不支援的 tooswitch 資料庫之間。 使用新連接 tooconnect tooa 不同的資料庫。 |
| 40510 |16 |陳述式 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援 |
| 40511 |16 |內建函數 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援。 |
| 40512 |16 |被取代的功能 '%ls' 在這個版本的 SQL Server 中不受支援。 |
| 40513 |16 |伺服器變數 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援。 |
| 40514 |16 |'%ls' 在這個版本的 SQL Server 中不受支援。 |
| 40515 |16 |參考 toodatabase 和/或伺服器名稱在 ' %.& #x2a; ls' 不支援此版本的 SQL Server。 |
| 40516 |16 |全域暫存物件在這個版本的 SQL Server 中不受支援。 |
| 40517 |16 |關鍵字或陳述式選項 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援。 |
| 40518 |16 |DBCC 命令 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援。 |
| 40520 |16 |安全性實體類別 '%S_MSG' 在這個版本的 SQL Server 中不受支援。 |
| 40521 |16 |在此版本的 SQL Server 中的 hello 伺服器範圍中不支援安全性實體類別 '%s_msg'。 |
| 40522 |16 |資料庫主體 '%.&#x2a;ls' 類型在這個版本的 SQL Server 中不受支援。 |
| 40523 |16 |隱含使用者 '%.&#x2a;ls' 建立在這個版本的 SQL Server 中不受支援。 明確建立 hello 使用者之後再使用它。 |
| 40524 |16 |資料型別 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援。 |
| 40525 |16 |WITH '%.ls' 在這個版本的 SQL Server 中不受支援。 |
| 40526 |16 |'%.&#x2a;ls' 資料列集提供者在這個版本的 SQL Server 中不受支援。 |
| 40527 |16 |連結的伺服器在這個版本的 SQL Server 中不受支援。 |
| 40528 |16 |使用者不可對應的 toocertificates、 非對稱金鑰或在這個版本的 SQL Server 的 Windows 登入。 |
| 40529 |16 |模擬內容中的內建函數 '%.&#x2a;ls' 在這個版本的 SQL Server 中不受支援。 |
| 40532 |11 |無法開啟伺服器"%.& #x2a; ls"hello 登入所要求。 hello 登入失敗。 |
| 40553 |16 |hello 工作階段已終止，因為它過度使用記憶體。 請嘗試修改查詢 tooprocess 較少的資料列。<br/><br/>*注意：*減少 hello 數量`ORDER BY`和`GROUP BY`TRANSACT-SQL 程式碼中的作業有助於減少 hello 記憶體需求，您的查詢。 |
| 40604 |16 |無法不 CREATE/ALTER DATABASE，因為它會超過 hello hello 伺服器配額。 |
| 40606 |16 |附加資料庫在這個版本的 SQL Server 中不受支援。 |
| 40607 |16 |Windows 登入在這個版本的 SQL Server 中不受支援。 |
| 40611 |16 |伺服器最多可以定義 128 個防火牆規則。 |
| 40614 |16 |防火牆規則的起始 IP 位址不能超過結束 IP 位址。 |
| 40615 |16 |無法開啟 '{0}' hello 登入所要求的伺服器。 IP 位址的用戶端 '{1}' 不允許 tooaccess hello 伺服器。  tooenable 存取使用 hello SQL 資料庫入口網站上或執行 sp_set_firewall_rule hello master 資料庫 toocreate 此 IP 位址或位址範圍的防火牆規則。  就會在此變更 tootake 效果 toofive 分鐘。 |
| 40617 |16 |hello 防火牆規則名稱開頭為<rule name>太長。 最大長度為 128。 |
| 40618 |16 |hello 防火牆規則名稱不可為空白。 |
| 40620 |16 |hello 登入失敗的使用者"%.& #x2a; ls"。 hello 密碼變更失敗。 在登入期間變更密碼在這個版本的 SQL Server 中不受支援。 |
| 40627 |20 |伺服器 '{0}' 和資料庫 '{1}' 上的作業正在進行中。 請稍候幾分鐘後再試一次。 |
| 40630 |16 |密碼驗證失敗。 hello 密碼不符合原則需求，因為它是太短。 |
| 40631 |16 |您指定的 hello 密碼名稱太長。 hello 密碼不可超過 128 個字元。 |
| 40632 |16 |密碼驗證失敗。 hello 密碼不符合原則需求，因為它不是不夠複雜。 |
| 40636 |16 |無法在此作業中使用保留的資料庫名稱 '%.&#x2a;ls'。 |
| 40638 |16 |無效的訂用帳戶識別碼 <subscription-id>。 訂用帳戶不存在。 |
| 40639 |16 |要求不符合 tooschema: <schema error>。 |
| 40640 |20 |hello 伺服器發生非預期的例外狀況。 |
| 40641 |16 |hello 指定的位置無效。 |
| 40642 |17 |hello 伺服器目前太過忙碌。 請稍後再試一次。 |
| 40643 |16 |hello 指定 x ms 版本標頭值無效。 |
| 40644 |14 |失敗的 tooauthorize 存取 toohello 指定訂用帳戶。 |
| 40645 |16 |Servername <servername> 不能是空白或 Null。 它可以只能由小寫字母 'a'-'z'、 hello 數字 0-9 和 hello 連字號。 hello 連字號不得或 hello 名稱結尾。 |
| 40646 |16 |訂用帳戶 ID 不能空白。 |
| 40647 |16 |訂用帳戶 <subscription-id> 沒有伺服器的伺服器名稱。 |
| 40648 |17 |已經執行太多要求。 請稍後重試。 |
| 40649 |16 |指定了無效的 Content-Type。 僅支援 application/xml。 |
| 40650 |16 |訂用帳戶 < 訂用帳戶 id > 不存在或尚未做好 hello 作業。 |
| 40651 |16 |因為 < 訂用帳戶 id > hello 訂用帳戶已停用失敗 toocreate 伺服器。 |
| 40652 |16 |無法移動或建立伺服器。 訂用帳戶 <subscription-id> 會超出伺服器配額。 |
| 40671 |17 |Hello 閘道與 hello 管理服務之間的通訊失敗。 請稍後重試。 |
| 40852 |16 |無法開啟資料庫 ' %。*ls' 上的 ' %。*hello 登入所要求的 ls'。 Access toohello 資料庫只允許使用已啟用安全性的連接字串。 此資料庫 tooaccess，修改您的連接字串 toocontain '安全' hello 伺服器 FQDN 為 '伺服器名稱'.database.windows.net 應修改的 too'server 名稱 ' 資料庫。`secure`。 windows.net。 |
| 45168 |16 |hello SQL Azure 系統負載，並置於單一伺服器的並行 DB CRUD 作業的時間上限 （例如，建立資料庫）。 hello hello 錯誤訊息中指定的伺服器已超過 hello 的並行連線數目上限。 請稍後再試。 |
| 45169 |16 |hello SQL azure 系統負載，並置於 hello 單一訂用帳戶的並行伺服器 CRUD 作業的數目上限 （例如，建立伺服器）。 hello 訂用帳戶指定 hello 錯誤訊息已超過 hello 的並行連線數目上限和 hello 要求遭到拒絕。 請稍後再試。 |

## <a name="related-links"></a>相關連結
* [Azure SQL Database 功能](sql-database-features.md)
* [Azure SQL Database 資源限制](sql-database-resource-limits.md)

