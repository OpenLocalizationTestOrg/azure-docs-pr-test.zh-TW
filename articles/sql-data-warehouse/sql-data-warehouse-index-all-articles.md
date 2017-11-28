---
title: "SQL 資料倉儲服務 aaaAll 主題 |Microsoft 文件"
description: "資料表的所有主題 hello Azure 服務的名稱存在於 http://azure.microsoft.com/documentation/articles/、 標題和描述的 SQL 資料倉儲。"
services: sql-data-warehouse
documentationcenter: 
author: barbkess
manager: jhubbard
editor: 
ms.assetid: a26a6dec-9c08-4415-8f58-4ee1dd41f718
ms.service: sql-data-warehouse
ms.workload: sql-data-warehouse
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: reference
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: 6f71d35b76b50764a5904525445675dafaa56b85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="all-topics-for-azure-sql-data-warehouse-service"></a>Azure SQL 資料倉儲服務的所有主題
本主題列出每個主題，適用於直接 toohello **SQL 資料倉儲**的 Azure 服務。 您可以使用來搜尋此網頁關鍵字**Ctrl + F**，目前的感興趣的 toofind hello 主題。

## <a name="new"></a>新增
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 1 |[SQL 資料倉儲備份](sql-data-warehouse-backups.md) |了解 SQL 資料倉儲內建的資料庫備份可讓您 toorestore Azure SQL 資料倉儲 tooa 還原點不同的地理區域。 |

## <a name="updated-articles-sql-data-warehouse"></a>更新的文章, SQL 資料倉儲
此區段會列出最近已更新的發行項，其中 hello 更新為大或重大。 對於每個更新的發行項，hello 的粗略程式碼片段會加入 markdown 文字會顯示。 hello 文件已更新的 hello 日期範圍內**2016年-08-22**太**2016年-10-05**。

| &nbsp; | 文章 | 更新的文字、程式碼片段 | 更新時機 |
| ---:|:--- |:--- |:--- |
| 2 |[從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |/-tootrack 位元組和選取 r.command、 s.request_id、 r.status，nbr_files 為計數 (相異 input_name)、 sum (s.bytes_processed) / 1024年/1024 gb_processed 從 sys.dm_pdw_exec_requests r join< sys.dm_pdw_dms_external_work s r.request_id 上為的檔案= s.request_id WHERE r。 label  = 'CTAS : Load  cso . DimProduct  '  OR r. label  = 'CTAS : Load  cso . FactOnlineSales  ' GROUP BY  r.command,  s.request_id,  r.status ORDER BY  nbr_files desc,  gb_processed desc; |2016-09-07 |
| 3 |[SQL 資料倉儲還原](sql-data-warehouse-restore-database-overview.md) |* * 可以將還原的已暫停的資料倉儲？ * * toorestore 已暫停的資料倉儲，您需要 toofirst 將其恢復上線。 Hello 資料倉儲回到線上之後，您必須從還原點 toochoose 七天。 * * 還原 tooa 備援地理區域 * * 如果您使用 hello 地理備援儲存體，您可以還原 hello 資料倉儲 tooyour 成對的資料中心中不同的地理區域。 hello 資料倉儲是從 hello 的最後一個每日備份還原。 * * 還原時間軸 * * 您可以還原資料庫 tooany 還原點內 hello 過去七天。 快照集開始每四個 tooeight 小時，且有七天。 當快照集存在時間超過七天，它就會過期，而且無法再使用其還原點。 * * 的 hello 還原資料倉儲 hello Azure 高階儲存體費率計費，還原成本 * * hello 儲存體費用。 如果您暫停還原的資料倉儲時，您將支付儲存體費率 hello Azure 高階儲存體。 暫停的 hello 優點是您不是免費 |2016-09-29 |

## <a name="get-started"></a>開始使用
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 4 |[驗證 tooAzure SQL 資料倉儲](sql-data-warehouse-authentication.md) |Azure Active Directory (AAD) 與 SQL Server 驗證 tooAzure SQL 資料倉儲。 |
| 5 |[Azure SQL 資料倉儲最佳做法](sql-data-warehouse-best-practices.md) |開發 Azure SQL 資料倉儲的解決方案時應該知道的建議和最佳作法。 這些可協助您成功。 |
| 6 |[適用於 Azure SQL 資料倉儲的驅動程式](sql-data-warehouse-connection-strings.md) |適用於 SQL 資料倉儲的連接字串和驅動程式 |
| 7 |[連接 tooAzure SQL 資料倉儲](sql-data-warehouse-connect-overview.md) |如何 toofind hello 伺服器名稱和連接字串，您 tooAzure SQL 資料倉儲 |
| 8 |[使用 Azure Machine Learning 分析資料](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md) |使用 Azure 機器學習 toobuild 預測機器學習模型根據儲存在 Azure SQL 資料倉儲中的資料。 |
| 9 |[查詢 Azure SQL 資料倉儲 (sqlcmd)](sql-data-warehouse-get-started-connect-sqlcmd.md) |查詢 Azure SQL 資料倉儲與 hello sqlcmd 命令列公用程式。 |
| 10 |[使用 Transact-SQL (TSQL) 建立 SQL 資料倉儲資料庫](sql-data-warehouse-get-started-create-database-tsql.md) |了解如何 toocreate Azure SQL 資料倉儲與 TSQL |
| 11 |[如何 toocreate 支援票證 SQL 資料倉儲](sql-data-warehouse-get-started-create-support-ticket.md) |如何 toocreate 支援票證中 Azure SQL 資料倉儲。 |
| 12 |[使用 Azure Data Factory 載入資料](sql-data-warehouse-get-started-load-with-azure-data-factory.md) |了解使用 Azure Data Factory tooload 資料 |
| 13 |[在 SQL 資料倉儲中使用 PolyBase 載入資料](sql-data-warehouse-get-started-load-with-polybase.md) |了解有什麼 PolyBase 以及 toouse 會針對資料倉儲案例。 |
| 14 |[建立 Azure SQL 資料倉儲](sql-data-warehouse-get-started-provision.md) |了解如何 toocreate Azure SQL 資料倉儲中的 hello Azure 入口網站 |
| 15 |[使用 PowerShell 建立 SQL 資料倉儲](sql-data-warehouse-get-started-provision-powershell.md) |使用 PowerShell 建立 SQL 資料倉儲 |
| 16 |[使用 Power BI 視覺化資料](sql-data-warehouse-get-started-visualize-with-power-bi.md) |使用 Power BI 視覺化 SQL 資料倉儲資料 |
| 17 |[查詢 Azure SQL 資料倉儲 (Visual Studio)](sql-data-warehouse-query-visual-studio.md) |使用 Visual Studio 查詢 SQL 資料倉儲。 |

## <a name="develop"></a>開發
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 18 |[最佳化 SQL 資料倉儲的交易](sql-data-warehouse-develop-best-practices-transactions.md) |在 Azure SQL 資料倉儲中撰寫有效率交易更新的最佳作法指引 |
| 19 |[SQL 資料倉儲中的並行存取和工作負載管理](sql-data-warehouse-develop-concurrency.md) |了解 Azure SQL 資料倉儲中的並行存取和工作負載管理以開發解決方案。 |
| 20 |[在 SQL 資料倉儲中的 Create Table As Select (CTAS)](sql-data-warehouse-develop-ctas.md) |使用 hello 撰寫程式碼的秘訣建立資料表，當在 Azure SQL 資料倉儲中選取 (CTAS) 陳述式，來開發方案。 |
| 21 |[SQL 資料倉儲中的動態 SQL](sql-data-warehouse-develop-dynamic-sql.md) |使用 Azure SQL 資料倉儲中的動態 SQL 以開發解決方案的秘訣。 |
| 22 |[根據 SQL 資料倉儲中的選項分組](sql-data-warehouse-develop-group-by-options.md) |根據 Azure SQL 資料倉儲中的選項實作群組以便開發解決方案的秘訣。 |
| 23 |[使用 SQL 資料倉儲中的標籤 tooinstrument 查詢](sql-data-warehouse-develop-label.md) |使用 Azure SQL 資料倉儲中的標籤 tooinstrument 查詢，來開發方案的秘訣。 |
| 24 |[SQL 資料倉儲中的迴圈](sql-data-warehouse-develop-loops.md) |在 Azure SQL 資料倉儲中使用 Transact-SQL 迴圈及取代資料指標以開發解決方案的秘訣。 |
| 25 |[SQL 資料倉儲中的預存程序](sql-data-warehouse-develop-stored-procedures.md) |在 Azure SQL 資料倉儲中實作預存程序以便開發解決方案的秘訣。 |
| 26 |[SQL 資料倉儲中的交易](sql-data-warehouse-develop-transactions.md) |在 Azure SQL 資料倉儲中實作交易以便開發解決方案的秘訣。 |
| 27 |[SQL 資料倉儲中使用者定義的結構描述](sql-data-warehouse-develop-user-defined-schemas.md) |在 Azure SQL 資料倉儲中使用 Transact-SQL 結構描述開發解決方案的秘訣。 |
| 28 |[在 SQL 資料倉儲中指派變數](sql-data-warehouse-develop-variable-assignment.md) |在 Azure SQL 資料倉儲中指派 TRANSACT-SQL 變數以便開發解決方案的秘訣。 |
| 29 |[SQL 資料倉儲中的檢視](sql-data-warehouse-develop-views.md) |在 Azure SQL 資料倉儲中使用 Transact-SQL 檢視開發解決方案的秘訣。 |
| 30 |[SQL 資料倉儲的設計決策和程式碼撰寫技術](sql-data-warehouse-overview-develop.md) |SQL 資料倉儲的開發概念、設計決策、建議和程式碼撰寫技巧。 |

## <a name="manage"></a>管理
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 31 |[管理 Azure SQL 資料倉儲中的計算能力 (概觀)](sql-data-warehouse-manage-compute-overview.md) |Azure SQL 資料倉儲中的效能相應放大功能。 向外延展藉由調整 Dwu 或暫停和繼續計算資源 toosave 成本。 |
| 32 |[管理 Azure SQL 資料倉儲中的計算能力 (Azure 入口網站)](sql-data-warehouse-manage-compute-portal.md) |Azure 入口網站工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。 |
| 33 |[管理 Azure SQL 資料倉儲中的計算能力 (PowerShell)](sql-data-warehouse-manage-compute-powershell.md) |PowerShell 工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。 |
| 34 |[管理 Azure SQL 資料倉儲中的計算能力 (REST)](sql-data-warehouse-manage-compute-rest-api.md) |PowerShell 工作 toomanage 運算能力。 透過調整 DWU 以調整計算資源。 或者，您也可以暫停和繼續計算資源 toosave 成本。 |
| 35 |[管理 Azure SQL 資料倉儲中的計算能力 (T-SQL)](sql-data-warehouse-manage-compute-tsql.md) |藉由調整 Dwu TRANSACT-SQL (T-SQL) 工作 tooscale 外延展效能。 透過在非尖峰時間進行縮減以節省成本。 |
| 36 |[使用 DMV 監視工作負載](sql-data-warehouse-manage-monitor.md) |深入了解如何 toomonitor 您使用 Dmv 的工作負載。 |
| 37 |[管理 Azure SQL 資料倉儲中的資料庫](sql-data-warehouse-overview-manage.md) |管理 SQL 資料倉儲資料庫的概觀。 包含管理工具、DWU 與相應放大效能、疑難排解查詢效能、建立良好的安全性原則，以及從資料損毀或區域性停電還原資料庫。 |
| 38 |[監視 Azure SQL 資料倉儲中的使用者查詢](sql-data-warehouse-overview-manage-user-queries.md) |Hello 考量、 最佳做法及監視使用者在 Azure SQL 資料倉儲中的查詢工作的概觀 |
| 39 |[SQL 資料倉儲還原](sql-data-warehouse-restore-database-overview.md) |復原資料庫，以在 Azure SQL 資料倉儲中的 hello 資料庫還原選項的概觀。 |
| 40 |[還原 Azure SQL 資料倉儲 (入口網站)](sql-data-warehouse-restore-database-portal.md) |還原 Azure SQL 資料倉儲的 Azure 入口網站工作。 |
| 41 |[還原 Azure SQL 資料倉儲 (PowerShell)](sql-data-warehouse-restore-database-powershell.md) |還原 Azure SQL 資料倉儲的 PowerShell 工作。 |
| 42 |[還原 Azure SQL 資料倉儲 (REST API)](sql-data-warehouse-restore-database-rest-api.md) |還原 Azure SQL 資料倉儲的 REST API 工作。 |

## <a name="tables-and-indexes"></a>資料表與索引
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 43 |[SQL 資料倉儲中的資料表的資料類型](sql-data-warehouse-tables-data-types.md) |開始使用 Azure SQL 資料倉儲資料表的資料類型。 |
| 44 |[在 SQL 資料倉儲中散發資料表](sql-data-warehouse-tables-distribute.md) |開始在 Azure SQL 資料倉儲中散發資料表。 |
| 45 |[在 SQL 資料倉儲中編製資料表的索引](sql-data-warehouse-tables-index.md) |開始在 Azure SQL 資料倉儲中編製資料表的索引 |
| 46 |[SQL 資料倉儲中的資料表概觀](sql-data-warehouse-tables-overview.md) |開始使用 Azure SQL 資料倉儲資料表。 |
| 47 |[在 SQL 資料倉儲中分割資料表](sql-data-warehouse-tables-partition.md) |開始在 Azure SQL 資料倉儲中分割資料表。 |
| 48 |[管理 SQL 資料倉儲中的資料表的統計資料](sql-data-warehouse-tables-statistics.md) |開始使用 Azure SQL 資料倉儲中的資料表的統計資料。 |
| 49 |[SQL 資料倉儲中的暫存資料表](sql-data-warehouse-tables-temporary.md) |開始使用 Azure SQL 資料倉儲中的暫存資料表。 |

## <a name="integrate"></a>整合
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 50 |[搭配使用 Azure Data Factory 與 SQL 資料倉儲](sql-data-warehouse-integrate-azure-data-factory.md) |搭配使用 Azure Data Factory (ADF) 與 SQL 資料倉儲以便開發解決方案的秘訣。 |
| 51 |[搭配使用 Azure 機器學習服務與 SQL 資料倉儲](sql-data-warehouse-integrate-azure-machine-learning.md) |搭配使用 Azure 機器學習服務與 SQL 資料倉儲以便開發解決方案的秘訣。 |
| 52 |[搭配使用 Azure 串流分析與 SQL 資料倉儲](sql-data-warehouse-integrate-azure-stream-analytics.md) |搭配使用 Azure 串流分析與 SQL 資料倉儲以便開發解決方案的秘訣。 |
| 53 |[搭配使用 Power BI 與 SQL 資料倉儲](sql-data-warehouse-integrate-power-bi.md) |搭配使用 Power BI 與 Azure SQL 資料倉儲以便開發解決方案的秘訣。 |
| 54 |[以 SQL 資料倉儲來搭配運用其他服務](sql-data-warehouse-overview-integrate.md) |工具以及提供可與 SQL 資料倉儲整合之解決方案的合作夥伴。 |

## <a name="load"></a>載入
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 55 |[從 Azure blob 儲存體將資料載入 Azure SQL 資料倉儲 (Azure Data Factory)](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md) |了解使用 Azure Data Factory tooload 資料 |
| 56 |[從 Azure Blob 儲存體將資料載入 SQL 資料倉儲 (PolyBase)](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md) |了解如何 toouse PolyBase tooload 資料從 Azure 到 SQL 資料倉儲的 blob 儲存體。 從公用資料載入 hello Contoso 零售資料倉儲結構描述的一些資料表。 |
| 57 |[將資料從 SQL Server 載入 Azure SQL 資料倉儲 (AZCopy)](sql-data-warehouse-load-from-sql-server-with-azcopy.md) |您可以使用 bcp tooexport 資料從 SQL Server tooflat 檔案、 AZCopy tooimport 資料 tooAzure blob 儲存體和 PolyBase tooingest hello 資料至 Azure SQL 資料倉儲。 |
| 58 |[將資料從 SQL Server 載入 Azure SQL 資料倉儲 (一般檔案)](sql-data-warehouse-load-from-sql-server-with-bcp.md) |對於小型資料大小，使用 bcp tooexport 資料從 SQL Server tooflat 檔案和資料匯入 hello 直接在 Azure SQL 資料倉儲。 |
| 59 |[將資料從 SQL Server 載入 Azure SQL 資料倉儲 (SSIS)](sql-data-warehouse-load-from-sql-server-with-integration-services.md) |示範如何從各種不同的資料的 SQL Server Integration Services (SSIS) 封裝 toomove 資料 toocreate 來源 tooSQL 資料倉儲。 |
| 60 |[在 SQL 資料倉儲中使用 PolyBase 載入資料](sql-data-warehouse-load-from-sql-server-with-polybase.md) |您可以使用 bcp tooexport 資料從 SQL Server tooflat 檔案、 AZCopy tooimport 資料 tooAzure blob 儲存體和 PolyBase tooingest hello 資料至 Azure SQL 資料倉儲。 |
| 61 |[在 SQL 資料倉儲中使用 PolyBase 的指南](sql-data-warehouse-load-polybase-guide.md) |在 SQL 資料倉儲案例中使用 PolyBase 的指導方針和建議。 |
| 62 |[將範例資料載入 SQL 資料倉儲](sql-data-warehouse-load-sample-databases.md) |將範例資料載入 SQL 資料倉儲 |
| 63 |[使用 bcp 載入資料](sql-data-warehouse-load-with-bcp.md) |了解哪些 bcp 和如何 toouse 會針對資料倉儲案例。 |
| 64 |[將資料載入 Azure SQL 資料倉儲](sql-data-warehouse-overview-load.md) |了解 hello 常見的資料載入到 SQL 資料倉儲案例。 這包含使用 PolyBase、Azure Blob 儲存體、一般檔案及寄送磁碟。 您也可以使用協力廠商工具。 |

## <a name="migrate"></a>移轉
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 65 |[移轉您的 SQL 程式碼 tooSQL 資料倉儲](sql-data-warehouse-migrate-code.md) |移轉您的 SQL 程式碼 tooAzure SQL 資料倉儲來開發方案的提示。 |
| 66 |[移轉資料](sql-data-warehouse-migrate-data.md) |移轉您的資料 tooAzure SQL 資料倉儲來開發方案的提示。 |
| 67 |[資料倉儲移轉公用程式 (預覽)](sql-data-warehouse-migrate-migration-utility.md) |移轉 tooSQL 資料倉儲。 |
| 68 |[移轉您的結構描述 tooSQL 資料倉儲](sql-data-warehouse-migrate-schema.md) |移轉您的結構描述 tooAzure SQL 資料倉儲來開發方案的提示。 |
| 69 |[移轉您的方案 tooSQL 資料倉儲](sql-data-warehouse-overview-migrate.md) |讓您的方案 tooAzure SQL 資料倉儲平台的移轉指導方針。 |

## <a name="partners"></a>合作夥伴
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 70 |[SQL 資料倉儲商業智慧合作夥伴](sql-data-warehouse-partner-business-intelligence.md) |具有可支援「SQL 資料倉儲」之解決方案的協力廠商商業智慧合作夥伴清單。 |
| 71 |[SQL 資料倉儲資料整合合作夥伴](sql-data-warehouse-partner-data-integration.md) |具有可支援「Azure SQL 資料倉儲」之資料整合解決方案的協力廠商合作夥伴清單。 |
| 72 |[SQL 資料倉儲資料管理合作夥伴](sql-data-warehouse-partner-data-management.md) |具有可支援「SQL 資料倉儲」之解決方案的協力廠商資料管理合作夥伴清單。 |

## <a name="reference"></a>參考
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 73 |[SQL 資料倉儲的參考主題](sql-data-warehouse-overview-reference.md) |SQL 資料倉儲的參考內容連結。 |
| 74 |[適用於 SQL 資料倉儲的 PowerShell Cmdlet 和 REST API](sql-data-warehouse-reference-powershell-cmdlets.md) |尋找 Azure SQL 資料倉儲 hello 最上層的 PowerShell 指令程式包括如何 toopause 和繼續資料庫。 |
| 75 |[語言元素](sql-data-warehouse-reference-tsql-language-elements.md) |使用 SQL 資料倉儲的 hello TRANSACT-SQL 語言項目的連結 tooreference 內容的清單。 |
| 76 |[Transact-SQL 主題](sql-data-warehouse-reference-tsql-statements.md) |如需 SQL 資料倉儲所使用的 hello TRANSACT-SQL 主題的連結 tooreference 內容。 |
| 77 |[系統檢視表](sql-data-warehouse-reference-tsql-system-views.md) |連結 toosystem SQL 資料倉儲的檢視內容。 |

## <a name="security"></a>安全性
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 78 |[SQL 資料倉儲 -  下層用戶端對稽核和動態資料遮罩的支援](sql-data-warehouse-auditing-downlevel-clients.md) |了解 SQL 資料倉儲下層用戶端對資料稽核的支援 |
| 79 |[Azure SQL 資料倉儲中的稽核](sql-data-warehouse-auditing-overview.md) |開始使用 Azure SQL 資料倉儲中的稽核 |
| 80 |[開始使用 SQL 資料倉儲中的透明資料加密 (TDE)](sql-data-warehouse-encryption-tde.md) |SQL 資料倉儲中的透明資料加密 (TDE) |
| 81 |[開始使用透明資料加密 (TDE)](sql-data-warehouse-encryption-tde-tsql.md) |SQL 資料倉儲中的透明資料加密 (TDE) (T-SQL) |
| 82 |[保護 SQL 資料倉儲中的資料庫](sql-data-warehouse-overview-manage-security.md) |保護 Azure SQL 資料倉儲中的資料庫以便開發解決方案的秘訣。 |

## <a name="miscellaneous"></a>其他資訊
| &nbsp; | 課程名稱 | 說明 |
| ---:|:--- |:--- |
| 83 |[安裝適用於 SQL 資料倉儲的 Visual Studio 和 SSDT](sql-data-warehouse-install-visual-studio.md) |安裝適用於 Azure SQL 資料倉儲的 Visual Studio 和 SQL Server Development Tools (SSDT) |
| 84 |[移轉 tooPremium 儲存詳細資料](sql-data-warehouse-migrate-to-premium-storage.md) |移轉現有的 SQL 資料倉儲 toopremium 存放裝置的指示 |
| 85 |[開始使用威脅偵測](sql-data-warehouse-security-threat-detection.md) |Tooget 威脅偵測與啟動的方式 |
| 86 |[SQL 資料倉儲容量限制](sql-data-warehouse-service-capacity-limits.md) |SQL 資料倉儲的連接、資料庫、資料表及查詢最大值。 |
| 87 |[針對 Azure SQL 資料倉儲問題進行疑難排解](sql-data-warehouse-troubleshoot.md) |針對 Azure SQL 資料倉儲問題進行疑難排解。 |

