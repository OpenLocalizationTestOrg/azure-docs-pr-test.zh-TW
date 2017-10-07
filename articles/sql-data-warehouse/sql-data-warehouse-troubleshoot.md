---
title: "Azure SQL 資料倉儲 aaaTroubleshooting |Microsoft 文件"
description: "針對 Azure SQL 資料倉儲問題進行疑難排解。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 51f1e444-9ef7-4e30-9a88-598946c45196
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/30/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 3c53a39f77057fe0bcc053a0b896555abf397515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-sql-data-warehouse"></a>針對 Azure SQL 資料倉儲問題進行疑難排解
部分 hello 較常見的疑難排解問題，我們了解我們的客戶從本主題列出。

## <a name="connecting"></a>連接
| 問題 | 解決方案 |
|:--- |:--- |
| 使用者 'NT AUTHORITY\ANONYMOUS LOGON' 登入失敗。 (Microsoft SQL Server，錯誤：18456) |AAD 使用者嘗試 tooconnect toohello master 資料庫，但在 master 中沒有使用者時，就會發生此錯誤。  指定此問題的 toocorrect hello 想 tooconnect tooat 連線時間，或新增 hello 使用者 toohello master 資料庫的 SQL 資料倉儲。  如需詳細資訊，請參閱[安全性概觀][Security overview]一文。 |
| hello 伺服器主體"MyUserName"不能 tooaccess hello hello 目前安全性內容下的資料庫 「 主要 」。 無法開啟使用者預設資料庫。 登入失敗。 使用者 'MyUserName' 登入失敗。 (Microsoft SQL Server，錯誤：916) |AAD 使用者嘗試 tooconnect toohello master 資料庫，但在 master 中沒有使用者時，就會發生此錯誤。  指定此問題的 toocorrect hello 想 tooconnect tooat 連線時間，或新增 hello 使用者 toohello master 資料庫的 SQL 資料倉儲。  如需詳細資訊，請參閱[安全性概觀][Security overview]一文。 |
| CTAIP 錯誤 |當 hello SQL server master 資料庫，但不是在 hello SQL 資料倉儲資料庫中已建立登入，就會發生此錯誤。  如果您遇到這個錯誤，看看 hello[安全性概觀][ Security overview]發行項。  本文說明如何 toocreate 登入和使用者上建立 master，然後如何，使用者在 toocreate hello SQL 資料倉儲資料庫。 |
| 遭到防火牆封鎖 |Azure SQL database 會保護伺服器和資料庫層級防火牆 tooensure 只有已知的 IP 位址有存取 tooa 資料庫。 hello 防火牆是安全的預設值，這表示您必須明確啟用及 IP 位址或位址範圍，才能連線。  tooconfigure 防火牆存取，請依照下列中的 hello 步驟[伺服器防火牆存取的用戶端 IP 設定][ Configure server firewall access for your client IP]在 hello[佈建指示][Provisioning instructions]. |
| 無法與工具或驅動程式連線 |SQL 資料倉儲，建議使用[SSMS][SSMS]， [SSDT for Visual Studio][SSDT for Visual Studio]，或[sqlcmd] [sqlcmd] tooquery 您的資料。 如需驅動程式和連接 tooSQL 資料倉儲的詳細資訊，請參閱[驅動程式的 Azure SQL 資料倉儲][ Drivers for Azure SQL Data Warehouse]和[連接 tooAzure SQL 資料倉儲][Connect tooAzure SQL Data Warehouse]文件。 |

## <a name="tools"></a>工具
| 問題 | 解決方案 |
|:--- |:--- |
| Visual Studio 物件總管中遺漏 AAD 使用者 |這是已知的問題。  因應措施，檢視中的 hello 使用者[sys.database_principals][sys.database_principals]。  請參閱[驗證 tooAzure SQL 資料倉儲][ Authentication tooAzure SQL Data Warehouse] toolearn 深入了解使用 Azure Active Directory 向 SQL 資料倉儲。 |
|手動指令碼、 使用 hello 指令碼精靈，或透過 SSMS 連接會很緩慢、 無回應，或產生的錯誤| 請確定使用者已建立 hello master 資料庫中。 在指令碼選項中，也請確定 hello 引擎版本設定為 「 Microsoft Azure SQL 資料倉儲版本 」，而且引擎類型是 「 Microsoft Azure SQL 資料庫 」。|

## <a name="performance"></a>效能
| 問題 | 解決方案 |
|:--- |:--- |
| 查詢效能疑難排解 |如果您嘗試 tootroubleshoot 特定查詢，以啟動[學習如何 toomonitor 查詢][Learning how toomonitor your queries]。 |
| 查詢效能和計劃不佳通常是因為遺漏統計資料 |hello 最常見不佳的原因是效能的缺少在資料表的統計資料。  請參閱[維護資料表統計資料][ Statistics]的詳細資料 toocreate 統計資料以及它們是重大 tooyour 效能的原因。 |
| 並行存取低落/排入佇列的查詢偏少 |了解[工作負載管理][ Workload management]是很重要的順序 toounderstand 如何 toobalance 與並行的記憶體配置。 |
| 如何 tooimplement 最佳作法 |hello 最佳地方 toostart toolearn 方式 tooimprove 查詢效能是否[SQL 資料倉儲的最佳作法][ SQL Data Warehouse best practices]發行項。 |
| 如何 tooimprove 效能調整 |Hello 方案 tooimproving 效能有時是 toosimply 新增更多計算 power tooyour 查詢[調整您的 SQL 資料倉儲][Scaling your SQL Data Warehouse]。 |
| 索引品質不佳導致查詢效能不佳 |有時，查詢會因為[資料行存放區索引品質不佳][Poor columnstore index quality]而變慢。  請參閱此文件，如需詳細資訊和如何太[重建索引 tooimprove 區段品質][Rebuild indexes tooimprove segment quality]。 |

## <a name="system-management"></a>系統管理
| 問題 | 解決方案 |
|:--- |:--- |
| 因為伺服器可能會超過允許的 45000 資料庫交易單位配額的 hello 訊息 40847： 無法執行 hello 作業。 |請減少 hello [DWU] [ DWU] hello 資料庫的嘗試 toocreate 或[要求增加配額][request a quota increase]。 |
| 調查空間使用量 |請參閱[資料表大小][ Table sizes] toounderstand hello 空間使用量的系統。 |
| 協助管理資料表 |請參閱 hello[資料表概觀][ Overview]協助管理您的資料表發行項。  本文還包含更詳細主題的連結，例如[資料表的資料類型][Data types]、[散發資料表][Distribute]、[編製資料表的索引][Index]、[分割資料表][Partition]、[維護資料表統計資料][Statistics]和[暫存資料表][Temporary]。 |
|透明資料加密 (TDE) 進度列不會更新在 hello Azure 入口網站|您可以檢視透過 TDE hello 狀態[powershell](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption)。|

## <a name="polybase"></a>Polybase
| 問題 | 解決方案 |
|:--- |:--- |
| 因為資料列太大而載入失敗 |目前，Polybase 不支援大型的資料列。  這表示如果您的資料表包含 varchar （max）、 nvarchar （max） 或 varbinary （max），外部資料表不能使用的 tooload 您的資料。  目前載入的大型的資料列是透過 Azure Data Factory （與 BCP)、 Azure Stream Analytics、 SSIS、 BCP 或 hello.NET SQLBulkCopy 類別只支援。 未來版本將增加讓 PolyBase 支援大型資料列。 |
| 使用 bcp 載入含有 MAX 資料類型的資料表失敗 |沒有其需要 varchar （max）、 nvarchar （max） 或 varbinary （max） 會放置在 hello 結尾 hello 資料表在某些案例中的已知的問題。  請嘗試移動您最大資料行 toohello hello 資料表結尾。 |

## <a name="differences-from-sql-database"></a>與 SQL Database 不同之處
| 問題 | 解決方案 |
|:--- |:--- |
| 不支援的 SQL Database 功能 |請參閱[不支援的資料表功能][Unsupported table features]。 |
| 不支援的 SQL Database 資料類型 |請參閱[不支援的資料類型][Unsupported data types]。 |
| DELETE 和 UPDATE 限制 |請參閱[更新因應措施][UPDATE workarounds]，[刪除因應措施][ DELETE workarounds]和[不支援更新前後使用 CTAS toowork 和DELETE 語法][Using CTAS toowork around unsupported UPDATE and DELETE syntax]。 |
| 不支援 MERGE 陳述式 |請參閱 [MERGE 因應措施][MERGE workarounds]。 |
| 預存程序限制 |請參閱[預存程序限制][ Stored procedure limitations] toounderstand 的某些 hello 預存程序的限制。 |
| UDF 不支援 SELECT 陳述式 |這是 UDF 目前的限制。  請參閱[CREATE FUNCTION] [ CREATE FUNCTION] hello 我們支援的語法。 |

## <a name="next-steps"></a>後續步驟
如果您已無法 toofind 方案 tooyour 問題上方，這裡有一些您可以嘗試的其他資源。

* [部落格]
* [功能要求]
* [影片]
* [CAT 小組部落格]
* [建立支援票證]
* [MSDN 論壇]
* [Stack Overflow 論壇]
* [Twitter]

<!--Image references-->

<!--Article references-->
[Security overview]: ./sql-data-warehouse-overview-manage-security.md
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx
[SSDT for Visual Studio]: ./sql-data-warehouse-install-visual-studio.md
[Drivers for Azure SQL Data Warehouse]: ./sql-data-warehouse-connection-strings.md
[Connect tooAzure SQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[建立支援票證]: ./sql-data-warehouse-get-started-create-support-ticket.md
[Scaling your SQL Data Warehouse]: ./sql-data-warehouse-manage-compute-overview.md
[DWU]: ./sql-data-warehouse-overview-what-is.md
[request a quota increase]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Learning how toomonitor your queries]: ./sql-data-warehouse-manage-monitor.md
[Provisioning instructions]: ./sql-data-warehouse-get-started-provision.md
[Configure server firewall access for your client IP]: ./sql-data-warehouse-get-started-provision.md#create-a-server-level-firewall-rule-in-the-azure-portal
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[Table sizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries
[Unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[Unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Poor columnstore index quality]: ./sql-data-warehouse-tables-index.md#causes-of-poor-columnstore-index-quality
[Rebuild indexes tooimprove segment quality]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Workload management]: ./sql-data-warehouse-develop-concurrency.md
[Using CTAS toowork around unsupported UPDATE and DELETE syntax]: ./sql-data-warehouse-develop-ctas.md#using-ctas-to-work-around-unsupported-features
[UPDATE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-update-statements
[DELETE workarounds]: ./sql-data-warehouse-develop-ctas.md#ansi-join-replacement-for-delete-statements
[MERGE workarounds]: ./sql-data-warehouse-develop-ctas.md#replace-merge-statements
[Stored procedure limitations]: ./sql-data-warehouse-develop-stored-procedures.md#limitations
[Authentication tooAzure SQL Data Warehouse]: ./sql-data-warehouse-authentication.md
[Working around hello PolyBase UTF-8 requirement]: ./sql-data-warehouse-load-polybase-guide.md#working-around-the-polybase-utf-8-requirement

<!--MSDN references-->
[sys.database_principals]: https://msdn.microsoft.com/library/ms187328.aspx
[CREATE FUNCTION]: https://msdn.microsoft.com/library/mt203952.aspx
[sqlcmd]: https://azure.microsoft.com/en-us/documentation/articles/sql-data-warehouse-get-started-connect-sqlcmd/

<!--Other Web references-->
[部落格]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[CAT 小組部落格]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[功能要求]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN 論壇]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse
[Stack Overflow 論壇]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[影片]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
