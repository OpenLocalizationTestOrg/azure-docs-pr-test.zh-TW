---
title: "aaaWhat 是 hello Azure SQL Database 服務嗎？ | Microsoft Docs"
description: "取得資料庫的簡介 tooSQL： 技術詳細資料和功能的關聯式資料庫管理系統 (RDBMS) hello 雲端中的。"
keywords: "簡介 toosql、 簡介 toosql，什麼是 sql 資料庫"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: cgronlun
ms.assetid: c561f600-a292-4e3b-b1d4-8ab89b81db48
ms.service: sql-database
ms.custom: overview
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 06/30/2017
ms.author: carlrab
ms.openlocfilehash: 24ca383ad7e140133d19debc8899f172ee4aa424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-sql-database-service"></a>什麼是 hello Azure SQL Database 服務？ 

SQL Database 是 Microsoft Azure 中一般用途的關聯式資料庫服務，可支援關聯式資料、JSON、空間和 XML 等結構。 它可提供[動態可調式效能](sql-database-service-tiers.md)，而且提供[資料行存放區索引](https://docs.microsoft.com/sql/relational-databases/indexes/columnstore-indexes-overview)等選項來進行極限分析和報告，以及[記憶體內部 OLTP](sql-database-in-memory.md) 來進行極限交易處理。 Microsoft 會處理所有修補和更新 hello SQL 程式碼基底的順暢地與抽象化 hello 基礎基礎結構的所有管理。 

SQL Database 與 hello 共用其程式碼基底[Microsoft SQL Server 資料庫引擎](https://docs.microsoft.com/sql/sql-server/sql-server-technical-documentation)。 與 Microsoft 的雲端優先策略，發行的第一個 tooSQL 資料庫，然後再 tooSQL 伺服器本身有 hello 的 SQL Server 的最新功能。 此方法提供您以 hello 最新的 SQL Server 功能沒有額外負荷會進行修補或升級-和使用這些新功能進行測試包含數百萬個資料庫。 當新功能宣佈時，如需其相關資訊，請參閱：

- **[Azure SQL database 的藍圖](https://azure.microsoft.com/roadmap/?category=databases)**: 位置 toofind 出最新消息和未來下一步。 
- **[Azure SQL Database 部落格](https://azure.microsoft.com/blog/topics/database)**：SQL Server 產品團隊成員發表 SQL Database 消息和功能的地方。 

SQL Database 提供多個服務等級的可預測效能，這可提供無停機時間的動態延展性、內建智慧型最佳化、全域延展性和可用性，以及進階安全性選項，且全都幾乎免管理。 這些功能可讓您快速的應用程式開發和加速您的時間 toomarket，而不是配置寶貴的時間和資源 toomanaging 虛擬機器和基礎結構上 toofocus。 hello SQL Database 服務目前為 38 的資料中心 hello world，具有多個資料中心上線定期，可讓您 toorun 靠近您資料中心中的資料庫。

> [!NOTE]
> 如需 Azure 平台安全性的相關資訊，請參閱 [Azure 信任中心](https://azure.microsoft.com/support/trust-center/security/)。
>

## <a name="scalable-performance-and-pools"></a>可擴充的效能和集區

採用 SQL Database，每個資料庫會彼此隔離並且可攜，每個都有自己的[服務層](sql-database-service-tiers.md)和保證的效能層級。 SQL Database 會針對不同的需求，提供不同的效能層級，並讓的資料庫 toobe 管理的集區 toomaximize hello 使用的資源，並節省成本。

### <a name="adjust-performance-and-scale-without-downtime"></a>無須停機即可調整效能和規模

SQL Database 提供四個服務層 toosupport tooheavyweight 輕量型資料庫工作負載： Basic、 Standard、 Premium 和 Premium RS。 您可以在較低的成本每月的小型、 單一資料庫上建立第一個應用程式，然後再變更其服務層以手動方式或以程式設計方式在方案的任何時間 toomeet hello 需求。 您可以調整沒有停機時間 tooyour 應用程式或 tooyour 客戶的效能。 動態擴充性可讓資料庫 tootransparently 回應 toorapidly 資源需求，並可讓您 tooonly 支付 hello 的資源，您需要在需要時變更。

   ![調整大小](./media/sql-database-what-is-a-dtu/single_db_dtus.png)

### <a name="elastic-pools-toomaximize-resource-utilization"></a>彈性集區 toomaximize 資源使用量

許多企業和應用程式，所能 toocreate 單一資料庫以及撥效能向上或向下隨選即已足夠，特別是如果使用模式是相對的可預測。 但是，如果您有無法預期的使用模式，它可更難 toomanage 成本和商務模型。 [彈性集區](sql-database-elastic-pool.md)是設計的 toosolve 這個問題。 hello 概念很簡單。 您配置效能資源 tooa 集區，而不是個別的資料庫，並支付 hello 整體效能 hello 集區的資源而不是單一資料庫效能。 

   ![彈性集區](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

使用彈性集區，您不需要在撥號增加和減少的資料庫效能，因為資源的要求有 toofocus。 hello 管理的集區資料庫取用 hello 效能資源 hello 彈性集區視需要。 管理的集區的資料庫使用，但不要超過 hello 限制 hello 集區，因此成本仍然可預測，即使不使用個別的資料庫。 什麼是多個項目，您可以[加入和移除資料庫 toohello 集區](sql-database-elastic-pool-manage-portal.md)，調整您的應用程式從資料庫 toothousands，全部都在您控制的預算內很多。 您也可以控制 hello 最小值和最大資源在 hello 集區 tooensure hello 集區中的任何資料庫會使用所有的可用 toodatabases hello 資源集區和每個集區的資料庫有保證最少的資源。 toolearn 有關使用彈性集區，SaaS 應用程式的設計模式的詳細資訊請參閱[SQL Database 的多租用戶 SaaS 應用程式的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)。

### <a name="blend-single-databases-with-pooled-databases"></a>混合使用單一資料庫與集區中的資料庫

不論您要使用單一資料庫或彈性集區，都將不再受到限制。 您可以混合使用彈性集區中，單一資料庫並快速且輕鬆地變更單一資料庫或彈性集區的 hello 服務層 tooadapt tooyour 情況。 Hello 電源和 Azure 的範圍，您可以混合與比其他 Azure 服務使用 SQL Database toomeet 唯一的應用程式的設計需求、 成本的磁碟機和資源效率，並解除鎖定新商機。

### <a name="extensive-monitoring-and-alerting-capabilities"></a>廣泛的監視和警示功能

但您要如何比較 hello 單一資料庫及彈性集區的相對效能？ 當您撥向上和向下如何知道 hello 以滑鼠右鍵按一下 停止？ 使用 hello[內建的效能監視](sql-database-performance.md)和[警示](sql-database-insights-alerts-portal.md)結合 hello 效能評等為基礎的工具[單一資料庫的資料庫交易單位 (Dtu) 和彈性集區有彈性的 dtu 數 (Edtu)](sql-database-what-is-a-dtu.md)。 使用這些工具，您可以迅速瞭解的向上或向下調整根據您目前的 hello 影響或專案的效能需求。 如需詳細資訊，請參閱 [SQL Database 選項和效能：了解每個服務層中可用的項目](sql-database-service-tiers.md) 。

此外，SQL Database 可以[發出計量和診斷記錄](sql-database-metrics-diag-logging.md)以便進行監視。 您可以設定 SQL Database toostore 資源使用狀況、 背景工作和工作階段和連線到一個 Azure 資源：

- **Azure 儲存體**：用於封存大量遙測資料，價格低廉
- **Azure 事件中樞**：用於整合 SQL Database 遙測與自訂監視解決方案或管線
- **Azure Log Analytics**：適用於具有報告、警示及緩和功能的內建監視解決方案

    ![架構](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="availability-capabilities"></a>可用性功能

Azure 領先業界的 99.99% 可用性服務等級協定 [(SLA)](http://azure.microsoft.com/support/legal/sla/)(由 Microsoft 管理之資料中心的全球網路提供支援)，可協助讓您的應用程式 24 小時全年無休地運作。 此外，SQL Database 還提供內建[業務持續性和全域延展性](sql-database-business-continuity.md)功能，包括：

- **[自動備份](sql-database-automated-backups.md)**：SQL Database 會自動執行完整、差異及交易記錄備份。
- **[時間點還原](sql-database-recovery-using-backups.md)**: SQL Database 支援原點 tooany hello 自動備份的保留期限內的時間。
- **[作用中地理複寫](sql-database-geo-replication-overview.md)**: SQL Database 可讓您 tooconfigure toofour 可讀取次要複本上的相同資料庫中任一個 hello 或全域發佈 Azure 資料中心。  比方說，如果您有大量的並行的唯讀交易類別目錄資料庫的 SaaS 應用程式，使用作用中地理複寫 tooenable 全域讀取小數位數，並移除上 hello 主要是因為 tooread 工作負載的瓶頸。 
- **[容錯移轉群組](sql-database-geo-replication-overview.md)**: SQL Database 可讓您 tooenable 高可用性和負載平衡全域小數位數，包括透明的地理複寫和容錯移轉的資料庫與彈性集區的大型集。 容錯移轉群組，並使用最基本的管理負擔離開所有 hello 複雜監視、 路由及容錯移轉協調流程 tooSQL 資料庫的全域分散式 SaaS 應用程式作用中地理複寫可讓建立。

## <a name="built-in-intelligence"></a>內建智慧

使用 SQL 資料庫時，您會取得內建智慧，可協助您大幅減少執行和管理資料庫的 hello 成本，以及最大化效能和應用程式的安全性。 SQL Database 隨時都能工作負載執行百萬計的客戶，會收集並處理大量的遙測資料，同時也完全尊重 hello 幕後客戶隱私權。 Hello 服務可以了解並調整您的應用程式，各種演算法會持續評估 hello 遙測資料。 根據這項分析，hello 服務隨附於改善建議量身訂做的 tooyour 特定工作負載的效能。 

### <a name="automatic-performance-tuning"></a>自動效能調整

SQL Database 提供深入了解 hello 查詢，您需要 toomonitor。 SQL Database 藉以了解您資料庫的模式，並可讓您 tooadapt 資料庫結構描述 tooyour 工作負載。 SQL Database 會使用 [SQL Database Advisor](sql-database-advisor.md) 提供效能微調建議，您可以在其中檢閱微調動作並加以套用。 不過，持續監視資料庫是冗長乏味的艱辛工作，尤其是在處理許多資料庫時。 管理大量的資料庫可能是不可能 toodo 有效率地甚至具有所有可用的工具和 SQL Database 和 Azure 入口網站提供的報表。 而不是監視，並手動調整您的資料庫，您可能會考慮委派一些 hello 監視及調整動作 tooSQL 資料庫使用自動調整功能。 SQL Database 會自動套用建議，測試，並確認每個動作 tooensure hello 效能微調持續改善。 如此一來，SQL Database 會自動調整 tooyour 工作負載配合受控制且安全的方式。 自動調整表示 hello 對資料庫效能仔細監視及進行比較之前和之後微調的每個動作，而且如果 hello 效能無法改善時，才會還原 hello 調整動作。

今天，我們的合作夥伴執行多[SaaS 多租用戶應用程式](sql-database-design-patterns-multi-tenancy-saas-applications.md)SQL 資料庫最上層依賴在自動的效能微調 toomake 確定他們的應用程式一定會穩定且可預測的效能。 這項功能可大幅減少效能事件的 hello 晚上 hello 中間的 hello 的風險。 此外，因為其基底之客戶的部分也會使用 SQL Server，他們會使用 hello 提供的 SQL Database toohelp SQL Server 客戶的相同的索引建議。

SQL Database 中可用的自動調整層面有兩個：

- **[自動索引管理](sql-database-automatic-tuning.md#automatic-index-management)**：識別您的資料庫中應該新增的索引，以及應該移除的索引。
- **[自動計劃更正](sql-database-automatic-tuning.md#automatic-plan-choice-correction)**：識別有問題的計劃並修正 SQL 計劃效能問題 (即將推出，已可用於 SQL Server 2017)。

### <a name="adaptive-query-processing"></a>自適性查詢處理

我們也會加入 hello[彈性查詢處理](/sql/relational-databases/performance/adaptive-query-processing)系列功能 tooSQL 資料庫，包括多重陳述式資料表值函式，交錯的執行批次模式記憶體授與意見反應與批次模式適應性聯結. 每個彈性查詢處理功能適用於類似的 「 了解和調整 」 技術，進一步協助解決效能問題相關的 toohistorically 面臨的查詢最佳化問題。

### <a name="intelligent-threat-detection"></a>智慧型威脅偵測

 [SQL 威脅偵測](sql-database-threat-detection.md)運用[SQL Database 稽核](sql-database-auditing.md)toocontinuously 監視 Azure SQL 資料庫的潛在危險的嘗試 tooaccess 敏感性資料。 SQL 威脅偵測提供新的圖層的安全性，這可讓客戶 toodetect 及回應 toopotential 威脅，在發生異常的活動提供安全性警示。 一旦有可疑的資料庫活動、潛在弱點、SQL 插入式攻擊和異常資料庫存取模式發生，使用者就會收到警示。 SQL 威脅偵測警示提供可疑活動的詳細資訊和建議動作如何 tooinvestigate 和降低 hello 威脅。 使用者可以瀏覽 hello 可疑事件 toodetermine，如果嘗試 tooaccess，hello 事件結果違反，或利用 hello 資料庫中的資料。 威脅偵測會使簡單 tooaddress 潛在威脅 toohello 資料庫沒有 hello 需要 toobe 安全性專家或管理進階監視系統的安全性。

## <a name="advanced-security-and-compliance"></a>進階安全性與合規性

SQL Database 提供了各式各樣的[內建的安全性與相容性功能](sql-database-security-overview.md)toohelp 您的應用程式符合各種安全性和法規遵循需求。 

### <a name="auditing-for-compliance-and-security"></a>合規性和安全性稽核

[SQL Database 稽核](sql-database-auditing.md)追蹤資料庫事件並將事件寫入 Azure 儲存體帳戶中 tooan 稽核記錄檔。 稽核可協助您保持法規遵循、了解資料庫活動，以及深入了解可指出商務考量或疑似安全違規的不一致和異常。

### <a name="data-encryption-at-rest"></a>待用資料加密

SQL Database[透明資料加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)有助於保護 hello 威脅惡意活動所執行的即時加密與解密的 hello 資料庫相關聯的備份和交易記錄檔在靜止而不需要變更 toohello 應用程式。 從 2017 年 5 月開始，會使用透明資料加密 (TDE) 自動保護所有新建的 Azure SQL 資料庫。 TDE 是 SQL 的證明所需的許多防止儲存媒體的相容性的標準 tooprotect 靜態加密技術。 客戶可以管理 hello TDE 加密金鑰和其他機密資料安全且相容的方式，使用 Azure 金鑰保存庫。

### <a name="data-encryption-in-motion"></a>移動中資料加密

SQL Database 是 hello 只有資料庫系統 toooffer 保護機密資料，在途中待用和查詢處理期間的[永遠加密](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-database-engine)。 永遠加密已提供前所未有的資料業界優先安全性以抵抗涉及 hello 竊取的重要資料的缺口。 例如，透過永遠加密，客戶的信用卡號碼會加密狀態儲存在 hello 資料庫一律，即使查詢處理期間，允許解密 hello 點的使用授權的人員或應用程式，需要 tooprocess 該資料。

### <a name="dynamic-data-masking"></a>動態資料遮罩

[SQL Database 動態資料遮罩](sql-database-dynamic-data-masking-get-started.md)會限制機密資料暴露其 toonon 權限的使用者。 動態資料遮罩藉此協助防止未經授權的存取 toosensitive 資料啟用客戶 toodesignate 多少 hello 敏感性資料 tooreveal hello 應用程式層上的影響降至最低。 這是 hello hello 查詢結果集內的機密資料隱藏在指定的資料庫欄位，而 hello 資料庫中的 hello 資料不會變更以原則為基礎的安全性功能。

### <a name="row-level-security"></a>資料列層級安全性

[資料列層級安全性](https://docs.microsoft.com/sql/relational-databases/security/row-level-security)可讓客戶 toocontrol 存取 toorows 根據 hello 特性 hello 使用者執行查詢的資料庫資料表中 (例如群組成員資格或執行內容)。 資料列層級安全性 (RLS) 簡化 hello 設計和編碼您的應用程式中的安全性。 RLS 可讓您在資料列存取 tooimplement 限制。 例如，確保工作者只能存取相關 tootheir 部門的資料列，或限制客戶的資料存取 tooonly hello 資料相關的 tootheir 公司。

### <a name="azure-active-directory-integration-and-multi-factor-authentication"></a>Azure Active Directory 整合和多重要素驗證

SQL Database 可讓您 toocentrally 管理的資料庫使用者名稱和其他 Microsoft 服務的身分識別[Azure Active Directory 整合](sql-database-aad-authentication.md)。 這項功能簡化了權限管理並增強安全性。 Azure Active Directory 支援[多重要素驗證](sql-database-ssms-mfa-authentication.md)(MFA) tooincrease 資料和應用程式安全性同時支援單一登入程序。

### <a name="compliance-certification"></a>合規性認證

SQL Database 會參與定期稽核，並已經過數個合規性標準的認證。 如需詳細資訊，請參閱 hello [Microsoft Azure 信任中心](https://azure.microsoft.com/support/trust-center/)，您可以找到 hello 最新的清單其中[SQL 資料庫相容性認證](https://azure.microsoft.com/support/trust-center/services/)。

## <a name="easy-to-use-tools"></a>容易使用

SQL Database 讓應用程式的建置及維護更簡易也更有生產力。 SQL Database 可讓您進行的動作最 toofocus： 建置絕佳的應用程式。 您可以使用已經擁有的工具和技巧，在 SQL Database 中進行管理和開發。

- **[hello Azure 入口網站](https://portal.azure.com/)**： 的 web 應用程式來管理所有 Azure 服務 
- **[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)**: 免費、 可下載的用戶端來管理應用程式的任何 SQL 基礎結構，從 SQL Server tooSQL 資料庫
- **[Visual Studio 中的 SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)**：可下載的免費用戶端應用程式，可用於開發 SQL Server 關聯式資料庫、Azure SQL 資料庫、Integration Services 套件、Analysis Services 資料模型及 Reporting Services 報告。
- **[Visual Studio 程式碼](https://code.visualstudio.com/docs)**： 免費、 可下載的開放原始、 程式碼編輯器視窗、 macOS 和 Linux 支援擴充功能，包括 hello [mssql 延伸](https://aka.ms/mssql-marketplace)查詢在 Microsoft SQL ServerAzure SQL Database 和 SQL 資料倉儲。

SQL Database 支援使用 Python、 Java、 Node.js、 PHP、 Ruby、 和 hello MacOS 上的.NET、 Linux 及 Windows 建立應用程式。 SQL Database 支援 hello 相同[連線庫](sql-database-libraries.md)與 SQL Server。

## <a name="engage-with-hello-sql-server-engineering-team"></a>洽詢 hello SQL Server 工程團隊

- [DBA Stack Exchange](https://dba.stackexchange.com/questions/tagged/sql-server)：詢問資料庫管理問題
- [堆疊溢位](http://stackoverflow.com/questions/tagged/sql-server)：詢問開發問題
- [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)：詢問技術問題
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)：回報錯誤和要求功能
- [Reddit](https://www.reddit.com/r/SQLServer/)：討論 SQL Server

## <a name="next-steps"></a>後續步驟

- 請參閱 hello[定價頁面](https://azure.microsoft.com/pricing/details/sql-database/)的單一資料庫，以及彈性集區的成本比較和計算機。

- 這些快速開始的 tooget 您一開始，請參閱：

  - [在 hello Azure 入口網站中建立 SQL 資料庫](sql-database-get-started-portal.md)  
  - [建立 SQL database 以 hello Azure CLI](sql-database-get-started-cli.md)
  - [使用 PowerShell 建立 SQL Database](sql-database-get-started-powershell.md)

- 如需一組 Azure CLI 和 PowerShell 範例，請參閱︰
  - [SQL Database 的 Azure CLI 範例](sql-database-cli-samples.md)
  - [SQL Database 的 Azure PowerShell 範例](sql-database-powershell-samples.md)
