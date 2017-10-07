---
title: "aaaManage Azure SQL Database 的結構描述中的多租用戶應用程式 |Microsoft 文件"
description: "在使用 Azure SQL Database 的多租用戶應用程式中，管理多租用戶的結構描述"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: billgib; sstein
ms.openlocfilehash: ea946e556808dabd60dd39cb8173d0512d4bddec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-schema-for-multiple-tenants-in-hello-wingtip-saas-application"></a>多個租用戶 hello Wingtip SaaS 應用程式中管理結構描述

hello[第一個 Wingtip SaaS 教學課程](sql-database-saas-tutorial.md)顯示 hello 應用程式如何佈建租用戶資料庫和註冊 hello 目錄中。 就像任何應用程式，hello Wingtip SaaS 應用程式將持續改進，經過一段時間，與有時候會需要變更 toohello 資料庫。 變更可能包括新增或變更結構描述、 新增或變更的參考資料，以及例行的資料庫維護工作 tooensure 最佳應用程式效能。 與 SaaS 應用程式，這些變更需要 toobe 跨租用戶資料庫可能會大量以及部署中協調的方式。 這些變更 toobe 未來租用戶資料庫、 需要 toobe 併入 hello 佈建程序。

本教學課程會探討兩種案例-將參考資料更新部署的所有租用戶，並 retuning hello 上的索引，資料表包含 hello 參考資料。 hello[彈性作業](sql-database-elastic-jobs-overview.md)功能是使用的 tooexecute 這些作業的所有租用戶和 hello*黃金*新的資料庫做為範本使用的租用戶資料庫。

在本教學課程中，您了解如何：

> [!div class="checklist"]

> * 建立作業帳戶
> * 跨多個租用戶進行查詢
> * 更新所有租用戶資料庫中的資料
> * 針對所有租用戶資料庫中的資料表建立索引


toocomplete 符合本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* 已安裝最新版本的 SQL Server Management Studio (SSMS) hello。 [下載並安裝 SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

*本教學課程會使用有限的預覽 （彈性資料庫工作） 所 hello SQL Database 服務功能。如果您想 toodo 本教學課程，提供您的訂用帳戶 idtooSaaSFeedback@microsoft.com主旨 = 彈性作業預覽。您會收到確認訊息，已啟用您的訂用帳戶之後,[下載及安裝最新發行前版本工作 cmdlet hello](https://github.com/jaredmoo/azure-powershell/releases)。這是有限預覽版，如果有相關問題或需要支援，請連絡 SaaSFeedback@microsoft.com。*


## <a name="introduction-toosaas-schema-management-patterns"></a>簡介 tooSaaS 結構描述管理模式

hello 每個資料庫的單一租用戶 SaaS 模式在許多方面與所產生，hello 資料隔離的優點，但在 hello 同時介紹 hello 維護和管理多個資料庫的額外的複雜性。 [彈性作業](sql-database-elastic-jobs-overview.md)有助於管理工作的 hello SQL 資料層。 作業 toosecurely 可讓您和可靠地執行工作 （T-SQL 指令碼） 獨立於使用者互動或輸入，對資料庫的群組。 這個方法也有應用程式中的所有租用戶使用的 toodeploy 結構描述和一般參考資料變更。 彈性的工作也可以使用的 toomaintain*黃金*hello 資料庫副本使用 toocreate 新租用戶，確保它必定 hello 最新的結構描述和參考資料。

![畫面](media/sql-database-saas-tutorial-schema-management/schema-management.png)


## <a name="elastic-jobs-limited-preview"></a>彈性作業有限預覽版

新版本的「彈性作業」現在是 Azure SQL Database 的整合功能 (不需要額外的服務或元件)。 這個新的「彈性作業」版本目前處於有限預覽版狀態。 這個有限預覽版本目前支援 PowerShell toocreate 工作帳戶和 T-SQL toocreate 及管理工作。

> [!NOTE]
> *本教學課程會使用有限的預覽 （彈性資料庫工作） 所 hello SQL Database 服務功能。如果您想 toodo 本教學課程，提供您的訂用帳戶 idtooSaaSFeedback@microsoft.com主旨 = 彈性作業預覽。您會收到確認訊息，已啟用您的訂用帳戶之後,[下載及安裝最新發行前版本工作 cmdlet hello](https://github.com/jaredmoo/azure-powershell/releases)。這是有限預覽版，如果有相關問題或需要支援，請連絡 SaaSFeedback@microsoft.com。*

## <a name="get-hello-wingtip-application-scripts"></a>取得 hello Wingtip 應用程式指令碼

hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 [步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。

## <a name="create-a-job-account-database-and-new-job-account"></a>建立作業帳戶資料庫和新的作業帳戶

本教學課程要求您使用 PowerShell toocreate hello 工作帳戶資料庫與工作帳戶。 如同 MSDB 和 SQL 代理程式，彈性的工作會使用 Azure SQL 資料庫 toostore 工作定義、 工作狀態和歷程記錄。 一旦建立 hello 工作帳戶之後，您可以建立並立即監視作業。

1. 開啟...\\學習模組\\結構描述管理\\*示範 SchemaManagement.ps1*在 hello **PowerShell ISE**。
1. 按**F5** toorun hello 指令碼。

hello*示範 SchemaManagement.ps1*指令碼呼叫 hello*部署 SchemaManagement.ps1*指令碼 toocreate *S2*資料庫名為**jobaccount** hello 類別目錄伺服器上。 然後，它會建立 hello 工作帳戶，做為參數 toohello 工作帳戶建立呼叫傳遞 hello jobaccount 資料庫。

## <a name="create-a-job-toodeploy-new-reference-data-tooall-tenants"></a>建立工作 toodeploy 新增參考資料 tooall 租用戶

每個租用戶資料庫包含一組定義的事件裝載在法院 hello 種類的法院型別。 在此練習中，您會部署更新 tooall hello 租用戶資料庫 tooadd 兩個其他地點類型：*機車賽*和*游泳社團*。 這些地點的型別對應 toohello 看到 hello 租用戶事件應用程式中的背景影像。

按一下 [hello 法院類型] 下拉式清單功能表上，驗證只限於 10 個地點類型選項可用，並特別該 '機車賽' 和 '游泳社團' 不包含 hello 清單中。

現在讓我們來建立工作 tooupdate hello *VenueTypes* hello 租用戶的所有資料庫中資料表，並新增 hello 法院類型。

toocreate 新的工作，我們會使用一組工作的系統預存程序建立 hello 工作帳戶時，在 hello jobaccount 資料庫中建立。

1. 開啟 SSMS 並連接 toohello 類別目錄伺服器： 類別目錄-\<使用者\>。.database.windows.net 伺服器
1. 也連接 toohello 租用戶伺服器： tenants1-\<使用者\>。.database.windows.net
1. 瀏覽 toohello *contosoconcerthall* hello 上的資料庫*tenants1*伺服器和查詢 hello *VenueTypes*資料表 tooconfirm，*機車賽*和*游泳社團***不**hello [結果] 清單中。
1. 開啟 hello 檔案...\\學習模組\\結構描述管理\\DeployReferenceData.sql
1. 修改 hello 陳述式： 設定@wtpUser=&lt;使用者&gt;和取代部署 hello Wingtip 應用程式時使用的 hello 使用者值
1. 確認您是連接的 toohello jobaccount 資料庫，然後按**F5**執行 hello 指令碼

* **預存程序\_新增\_目標\_群組**建立 hello 目標群組名稱 DemoServerGroup，現在我們需要 tooadd 目標成員。
* **預存程序\_新增\_目標\_群組\_成員**新增*伺服器*目標成員類型，認為該伺服器 （請注意這是 hello tenants1內的所有資料庫&lt;使用者&gt;包含 hello 租用戶資料庫伺服器) 在工作時間執行應該包含在 hello 工作第二個新增 hello*資料庫*目標成員類型，特別是 hello '黃金' 資料庫 (basetenantdb) 位於類別目錄-&lt;使用者&gt;伺服器，以及最後的另一個*資料庫*目標群組成員型別 tooinclude hello adhocanalytics 資料庫之後的教學課程中所使用。
* **sp\_add\_job** 會建立稱為「參考資料部署」的作業
* **預存程序\_新增\_jobstep**會建立包含 T-SQL 命令文字 tooupdate hello 參考資料表中，VenueTypes hello 作業步驟
* hello 指令碼中的 hello 剩餘檢視會顯示 hello hello 物件和執行監視作業存在。 在 hello 中使用這些查詢 tooreview hello 狀態值**生命週期**時 hello 工作已順利完成所有租用戶資料庫與 hello 兩個其他資料庫包含 hello 參考資料表上的資料行 toodetermine。

1. 在 SSMS 中，瀏覽 toohello *contosoconcerthall* hello 上的資料庫*tenants1*伺服器和查詢 hello *VenueTypes*資料表 tooconfirm，*機車賽*和*游泳社團***是**現在 hello [結果] 清單中。


## <a name="create-a-job-toomanage-hello-reference-table-index"></a>建立工作 toomanage hello 參考資料表索引

類似 toohello 上一個練習中，這個練習作業 toorebuild hello 上建立索引 hello 參考資料表主索引鍵，在一般資料庫管理作業的系統管理員可能會執行大型資料載入之後，插入資料表。

建立使用 hello 作業相同的作業 'system' 預存程序。

1. 開啟 SSMS 並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器
1. 開啟 hello 檔案...\\學習模組\\結構描述管理\\OnlineReindex.sql
1. 以滑鼠右鍵按一下、 選取連接，並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器，如果尚未連接
1. 請確定您已連線的 toohello jobaccount 資料庫，然後按 F5 toorun hello 指令碼

* sp\_add\_job 會建立稱為「線上 PK 索引重建\_\_VenueTyp\_\_265E44FD7FD4C885」的新作業
* 預存程序\_新增\_作業步驟會建立包含 T-SQL 命令文字 tooupdate hello 索引的 hello 作業步驟




## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]

> * 建立工作帳戶 tooquery 跨多個租用戶
> * 更新所有租用戶資料庫中的資料
> * 針對所有租用戶資料庫中的資料表建立索引

[臨機操作分析教學課程](sql-database-saas-tutorial-adhoc-analytics.md)


## <a name="additional-resources"></a>其他資源

* [Hello Wingtip SaaS 應用程式部署為基礎的其他教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [管理相應放大的雲端資料庫](sql-database-elastic-jobs-overview.md)
* [建立和管理相應放大的雲端資料庫](sql-database-elastic-jobs-create-and-manage.md)
