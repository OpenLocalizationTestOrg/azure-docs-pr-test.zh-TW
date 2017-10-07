---
title: "aaaSQL 資料庫應用程式開發概觀 |Microsoft 文件"
description: "了解可用的連接程式庫和連接 tooSQL 資料庫應用程式的最佳作法。"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: genemi
ms.assetid: 67c02204-d1bd-4622-acce-92115a7cde03
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: 17f04db600828f90c42c750c9abdb92cfa4ca817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-application-development-overview"></a>SQL Database 應用程式開發概觀
本文逐步 hello 開發人員應該注意撰寫程式碼 tooconnect tooAzure SQL Database 時的基本考量。

> [!TIP]
> 如需教學課程顯示您如何 toocreate 伺服器，建立伺服器型防火牆，檢視伺服器屬性，使用 SQL Server Management Studio，查詢 hello master 資料庫進行連接、 建立範例資料庫和一個空白資料庫、 查詢資料庫內容，連接使用 SQL Server Management Studio，而且查詢 hello 範例資料庫，請參閱[取得教學課程](sql-database-get-started-portal.md)。
>

## <a name="language-and-platform"></a>語言和平台
有一些程式碼範例可供各種程式設計語言和平台使用。 您可以找到連結 toohello 程式碼範例： 

* 詳細資訊： [SQL Database 和 SQL Server 的連線庫](sql-database-libraries.md)

## <a name="tools"></a>工具 
您可以利用 [cheetah](https://github.com/wunderlist/cheetah)、[sql-cli](https://www.npmjs.com/package/sql-cli)、[VS Code](https://code.visualstudio.com/) 等開放原始碼工具。 此外，Azure SQL Database 使用 [Visual Studio](https://www.visualstudio.com/downloads/) 和 [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) 等 Microsoft 工具。  您也可以使用 hello Azure 管理入口網站、 PowerShell 和 REST Api 可協助您獲得額外的產能。

## <a name="resource-limitations"></a>資源限制
Azure SQL Database 管理 hello 資源可用 tooa 資料庫使用兩個不同的機制： 資源控管和強制執行的限制。

* 詳細資訊： [Azure SQL Database 資源限制](sql-database-resource-limits.md)

## <a name="security"></a>安全性
Azure SQL Database 提供資源以在 SQL Database 上限制存取、保護資料，以及監視活動。

* 詳細資訊： [保護您的 SQL Database](sql-database-security-overview.md)

## <a name="authentication"></a>驗證
* Azure SQL Database 支援 SQL Server 驗證使用者和登入，以及 [Azure Active Directory 驗證](sql-database-aad-authentication.md) 使用者和登入。
* 您需要特定的資料庫，而不是正在 toohello toospecify*主要*資料庫。
* 您無法使用 hello TRANSACT-SQL**使用 myDatabaseName;** SQL Database tooswitch tooanother 資料庫上的陳述式。
* 詳細資訊： [SQL Database 安全性：管理資料庫存取與登入安全性](sql-database-manage-logins.md)

## <a name="resiliency"></a>復原功能
當連線 tooSQL 資料庫時，就會發生暫時性的錯誤時，您的程式碼應該重試 hello 呼叫。  建議重試邏輯使用輪詢邏輯，使它不會不會淹沒 hello SQL Database 與多個用戶端同時重試。

* 程式碼範例： 取得程式碼範例將示範中，然後重試邏輯，請參閱您選擇在 hello 語言的範例：[連接程式庫，針對 SQL Database 和 SQL Server](sql-database-libraries.md)
* 詳細資訊： [SQL Database 用戶端程式的錯誤訊息](sql-database-develop-error-messages.md)

## <a name="managing-connections"></a>管理連線
* 在您用戶端連線的邏輯，覆寫 hello 預設逾時 toobe 30 秒。  hello 預設值是 15 秒會太短，取決於的連接 hello 網際網路。
* 如果您使用[連接集區](http://msdn.microsoft.com/library/8xx3tyca.aspx)，是確定 tooclose hello 連接 hello 立即程式未主動使用它，並不準備 tooreuse 它。

## <a name="network-considerations"></a>網路考量事項
* Hello 電腦上裝載您的用戶端程式，確定 hello 防火牆允許連接埠 1433年上的傳出 TCP 通訊。  詳細資訊： [設定 Azure SQL Database 防火牆](sql-database-configure-firewall-settings.md)
* 如果您的用戶端會在 Azure 虛擬機器 (VM) 上執行時，用戶端程式會連接 tooSQL 資料庫，您必須開啟 hello VM 上的特定連接埠範圍。 詳細資訊：[針對 ADO.NET 4.5 和 SQL Database 之 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)
* 用戶端連線 tooAzure SQL 資料庫有時會略過 hello proxy，並與 hello 資料庫直接互動。 1433 以外的連接埠變得重要。 如需詳細資訊，請參閱 [Azure SQL Database 連線架構](sql-database-connectivity-architecture.md)和[針對 ADO.NET 4.5 及 SQL Database 的 1433 以外的連接埠](sql-database-develop-direct-route-ports-adonet-v12.md)一節。

## <a name="data-sharding-with-elastic-scale"></a>使用 Elastic Scale 的資料分區化
Elastic Scale 簡化 hello 的縮放比例外 （和） 的程序。 

* [多租用戶 SaaS 應用程式與 Azure SQL Database 的設計模式](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* [資料相依路由](sql-database-elastic-scale-data-dependent-routing.md)
* [開始使用 Azure SQL Database Elastic Scale 預覽](sql-database-elastic-scale-get-started.md)

## <a name="next-steps"></a>後續步驟
瀏覽所有 hello [SQL Database 的功能](sql-database-technical-overview.md)
