---
title: "Azure SQL 資料倉儲中的 aaaManage 資料庫 |Microsoft 文件"
description: "管理 SQL 資料倉儲資料庫的概觀。 包含管理工具、DWU 與相應放大效能、疑難排解查詢效能、建立良好的安全性原則，以及從資料損毀或區域性停電還原資料庫。"
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a>管理 Azure SQL 資料倉儲中的資料庫
SQL 資料倉儲會自動化管理您的資料庫的各個層面。 比方說，tooscale 效能，您只需要 tooadjust 和支付 hello 運算資源的權限層級，然後讓 SQL 資料倉儲執行所有的 hello 工作的向外延展和向後還原作業。

您一定想 toomonitor 您的工作負載 tooidentify 您效能需求，以及疑難排解長時間執行的查詢。 您也需要 tooperform 一些安全性工作 toomanage 權限的使用者與登入。

本概觀涵蓋管理 SQL 資料倉儲的這些層面。

* 管理工具
* 調整計算
* 暫停與繼續
* 效能最佳作法
* 查詢監控
* Security
* 備份與還原

## <a name="management-tools"></a>管理工具
您可以使用各種工具 toomanage 資料庫在 SQL 資料倉儲中。 因為您管理資料庫，您將開發工具喜好設定的每種工作類型，您需要 tooperform。

### <a name="azure-portal"></a>Azure 入口網站
hello [Azure 入口網站][ Azure portal]是網頁型入口網站，建立、 更新和刪除資料庫和監視資料庫資源。 此工具最適合是如果您剛開始使用 azure，管理少量的資料倉儲資料庫，或 tooquickly 需要執行一些動作。

tooget 入門 hello Azure 入口網站，請參閱[建立 SQL 資料倉儲 （Azure 入口網站）][Create a SQL Data Warehouse (Azure portal)]。

### <a name="sql-server-data-tools-in-visual-studio"></a>Visual Studio 中的 SQL Server Data Tools
[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) 在 Visual Studio 可讓您 tooconnect 來管理及開發您的資料庫。 如果您是熟悉 Visual Studio 或其他整合式開發環境 (IDE) 的應用程式開發人員，請嘗試使用 Visual Studio 中的 SSDT。

SSDT 包含 SQL Server 物件總管可讓您 toovisualize hello、 連線，並執行對 SQL 資料倉儲資料庫的指令碼。 tooquickly 連接 tooSQL 資料倉儲，您只需按一下 hello **Visual Studio 中開啟**hello Azure 傳統入口網站中檢視 hello 資料庫詳細資料時，hello 命令列中的按鈕。  

請參閱 < 開始使用 Visual Studio 中的 SSDT tooget[查詢 Azure SQL 資料倉儲與 Visual Studio][Query Azure SQL Data Warehouse with Visual Studio]。

### <a name="command-line-tools"></a>命令列工具
命令列工具非常適合自動化您的工作負載。  PowerShell 和 sqlcmd 是兩種方法皆適合 tooautomate 您的程序。  我們建議這些工具來管理大量的邏輯伺服器和部署在生產環境中的資源變更，可以編寫指令碼或然後自動化所需的 hello 工作。

### <a name="dynamic-management-views"></a>動態管理檢視
Dmv 會管理 SQL 資料倉儲的 hello bread and 奶油。 幾乎所有會呈現在 hello 入口網站中的資訊依賴 Dmv。 toosee 一份 SQL 資料倉儲 Dmv，請參閱[SQL 資料倉儲系統檢視表][SQL Data Warehouse system views]。

tooget 啟動，請參閱[連接和查詢使用 sqlcmd][Connect and query with sqlcmd]，和[建立資料庫 (PowerShell)][Create a database (PowerShell)]。

## <a name="scale-compute"></a>調整計算
在 SQL 資料倉儲中，您可以快速地將效能相應放大或調整回來，方法是增加或減少 CPU、記憶體和 I/O 頻寬的計算資源。 tooscale 效能，您只需要 toodo 正在調整 hello 資料倉儲單位 (Dwu) SQL 資料倉儲會配置 tooyour 資料庫數目。 SQL 資料倉儲快速變更的 hello 並處理所有的基礎變更 toohardware hello 或軟體。

toolearn 深入了解調整 dwu 調整，請參閱[調整效能]。

## <a name="pause-and-resume"></a>暫停與繼續
toosave 成本，您可以暫停和繼續計算資源隨。 例如，如果您將不會使用 hello 資料庫期間 hello 夜晚及週末，可以暫停在這些時間，並繼續 hello 一天。 您不需要支付費用的 Dwu hello 資料庫暫停時。

如需詳細資訊，請參閱[暫停計算][Pause compute]和[繼續計算][Resume compute]。

## <a name="performance-best-practices"></a>效能最佳作法
當開始使用新的技術，探索 hello 的秘訣和技巧可從 hello 開始最佳的權限可讓您很多時間。  您可以在許多主題中找到我們的最佳作法。

請參閱 toosee hello 最重要的考量開發您的工作負載時的許多摘要[SQL 資料倉儲的最佳作法][SQL Data Warehouse Best Practices]。

## <a name="query-monitoring"></a>查詢監控
有時候查詢太長，但您不確定哪一個 hello 問題。 SQL 資料倉儲具有動態管理檢視 (Dmv)，您可以使用 toofigure 出的查詢太長。

toofind 長時間執行的查詢，請參閱[監視您的工作負載使用 Dmv][Monitor your workload using DMVs]。

## <a name="security"></a>安全性
toomaintain 安全系統，您必須在 hello 警示並防範未經授權任何的存取型別。 安全性系統必須 toomake 確定防火牆規則已就緒，所以只有獲得授權的 IP 位址可以連線。 它需要使用者認證的適當驗證。 使用者已連接 toohello 資料庫之後，hello 使用者應該只有權限 tooperform 最少的動作。 toosecure 資料，您可以使用加密。 它也是重要 toohave 稽核與追蹤讓您可以追溯事件，如果沒有任何可疑的活動。

關於管理安全性，透過 toohello head toolearn[安全性概觀][Security overview]。

## <a name="backup-and-restore"></a>備份與還原
對生產環境資料庫來說，擁有可靠的資料備份是不可或缺的一部分。 「SQL 資料倉儲」會自動定期備份您的作用中資料庫來維護您的資料安全。 這些備份可讓您 toorecover 情況下，您已在此資料已損毀或意外遭到卸除資料庫或資料。  針對 hello 資料備份排程，請保留原則和如何 toorestore 資料庫，請參閱[從快照還原][Restore from snapshot]。

## <a name="next-steps"></a>後續步驟
使用良好的資料庫設計原則可以讓您更容易 toomanage SQL 資料倉儲資料庫。 toolearn 詳細，透過 toohello head[開發概觀][Development overview]。

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[調整效能]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
