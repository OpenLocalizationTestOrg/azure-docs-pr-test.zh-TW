---
title: "aaaIntro Wingtip SaaS-Azure SQL Database 多租用戶應用程式 |Microsoft 文件"
description: "使用範例多租用戶應用程式使用 Azure SQL Database，hello Wingtip SaaS 應用程式，了解"
keywords: SQL Database Azure
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>簡介 toohello Wingtip SaaS 應用程式

hello *Wingtip SaaS*應用程式是範例多租用戶應用程式，示範 hello 的 SQL Database 的獨特好處。 hello 應用程式會使用資料庫的各個租用戶，SaaS 應用程式模式 tooservice 多個租用戶。 hello 應用程式是 Azure SQL Database 的設計的 tooshowcase 功能可讓 SaaS 案例，包括數個 SaaS 設計和管理模式。 tooquickly 啟動和執行，請在五分鐘內部署 hello Wingtip SaaS 應用程式 ！

應用程式來源的程式碼和管理指令碼位於 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 toorun hello 指令碼，[下載 hello 學習模組資料夾](#download-and-unblock-the-wingtip-saas-scripts)tooyour 本機電腦。

## <a name="sql-database-wingtip-saas-tutorials"></a>SQL Database Wingtip SaaS 教學課程

部署之後 hello 應用程式，請瀏覽 hello 遵循 hello 初始部署為基礎的教學課程。 這些教學課程會探索常見 SaaS 模式，其利用 SQL Database、SQL 資料倉儲和其他 Azure 服務的內建功能。 教學課程包含詳細的說明，大幅簡化了解，以 PowerShell 指令碼，並實作 hello 在應用程式中的相同 SaaS 管理模式。


| 教學課程 | 說明 |
|:--|:--|
|[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)| **從這裡開始！** 部署及瀏覽 hello Wingtip SaaS 應用程式 tooyour Azure 訂用帳戶。 |
|[佈建租用戶並在目錄中註冊](sql-database-saas-tutorial-provision-and-catalog.md)| Hello 應用程式如何連接 tootenants 使用類別目錄資料庫，了解，以及如何 hello 目錄對應的租用戶 tootheir 資料。 |
|[監視及管理效能](sql-database-saas-tutorial-performance-monitoring.md)| 了解如何 toouse 監視功能的 SQL Database 和如何 tooset 警示時超出效能臨界值。 |
|[透過 Log Analytics (OMS) 監視](sql-database-saas-tutorial-log-analytics.md) | 了解如何使用[記錄分析](../log-analytics/log-analytics-overview.md)toomonitor 大量的資源，跨多個集區。 |
|[還原單一租用戶](sql-database-saas-tutorial-restore-single-tenant.md)| 了解如何 toorestore 租用戶資料庫 tooa 先前時間點。 步驟 toorestore tooa 平行資料庫，讓 hello 現有租用戶資料庫上線，也會包含。 |
|[管理租用結構描述](sql-database-saas-tutorial-schema-management.md)| 了解如何 tooupdate 結構描述，並更新參考資料，跨所有 Wingtip SaaS 租用戶。 |
|[執行臨機操作分析](sql-database-saas-tutorial-adhoc-analytics.md) | 建立臨機操作分析資料庫並對所有租用戶執行即時分散式查詢。  |
|[執行租用戶分析](sql-database-saas-tutorial-tenant-analytics.md) | 將租用戶資料擷取到分析資料庫或資料倉儲中，以便執行離線分析查詢。 |



## <a name="application-architecture"></a>應用程式架構

hello Wingtip SaaS 應用程式使用 hello 資料庫每個租用戶模型，並使用 SQL 彈性集區 toomaximize 效率。 佈建及租用戶 tootheir 資料對應，目錄會使用資料庫。 hello 核心 Wingtip SaaS 應用程式，使用具有三個範例租用戶，再加上 hello 類別目錄資料庫集區。 完成許多 hello Wingtip SaaS 教學課程會導致附加元件 toohello 初始部署後，藉由引進分析資料庫，跨資料庫結構描述管理等等。


![Wingtip SaaS 架構](media/sql-database-wtp-overview/app-architecture.png)


時經過 hello 教學課程和使用 hello 應用程式，它會是重要 toofocus hello SaaS 模式會彼此 toohello 資料層。 換句話說，著重於 hello 資料層，而不要超過分析 hello 應用程式本身。 了解這些 SaaS 模式 hello 實作是金鑰 tooimplementing 這些模式，在應用程式中的，同時考慮到特定的業務需求的任何必要的修改。

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>下載並解除封鎖 hello Wingtip SaaS 指令碼

從外部來源下載 zip 檔案並進行解壓縮時，Windows 可能會封鎖可執行的內容 (指令碼、dll)。 從 zip 檔案解壓縮 hello 指令碼時***步驟 hello 下方 toounblock hello.zip 檔案，然後才能擷取***。 這可確保會允許 toorun hello 指令碼。

1. 瀏覽過[hello Wingtip SaaS github 儲存機制](https://github.com/Microsoft/WingtipSaaS)。
1. 按一下 [複製或下載]。
1. 按一下**Download ZIP**儲存 hello 檔案。
1. 以滑鼠右鍵按一下 hello **WingtipSaaS master.zip**檔案，然後選取**屬性**。
1. 在 hello**一般**索引標籤上，選取**解除封鎖**。
1. 按一下 [確定] 。
1. Hello 檔案解壓縮。

指令碼位於 hello *...\\WingtipSaaS master\\學習模組*資料夾。


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>使用 hello Wingtip SaaS PowerShell 指令碼

tooget hello 最 hello 範例超出您需要 toodive hello 提供指令碼。 使用中斷點和逐步執行 hello 指令碼，檢查 hello hello SaaS 模式不同的實作方式的詳細資料。 tooeasily 逐步執行 hello 提供指令碼和模組 hello 最好了解，我們建議您使用 hello [PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise)。

### <a name="update-hello-configuration-file-for-your-deployment"></a>更新您的部署的 hello 設定檔

編輯 hello **UserConfig.psm1** hello 資源群組和使用者值與您在部署期間設定的檔案：

1. 開啟 hello *PowerShell ISE*並載入...\\學習模組\\*UserConfig.psm1* 
1. 更新*ResourceGroupName*和*名稱*（位於行 10 和 11 只） 部署的 hello 特定值。
1. 儲存 hello 變更 ！

這裡設定這些值只可防止您在每個指令碼中具有 tooupdate 這些部署專屬的值。

### <a name="execute-scripts-by-pressing-f5"></a>按 F5 執行指令碼

使用數個指令碼*$PSScriptRoot* toonavigate 資料夾和*$PSScriptRoot*藉由按下執行指令碼時，才會評估**F5**。  醒目提示並執行選取項目 (**F8**) 可能會導致錯誤，因此請在執行指令碼時按 **F5**。

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>逐步執行 hello 指令碼 tooexamine hello 實作

hello 最佳方式 toounderstand hello 指令碼會透過逐步執行它們 toosee 它們執行的動作。 簽出 hello 包含**示範-**呈現輕鬆 toofollow 高階工作流程的指令碼。 hello**示範-**指令碼顯示 hello 步驟需要的 tooaccomplish 每項工作，因此設定中斷點，而且會鑽研更深入 hello 個別呼叫 toosee 實作細節 hello SaaS 模式不同。

探索及逐步執行 PowerShell 指令碼的秘訣：

* 開啟**示範-** hello PowerShell ISE 中的指令碼。
* 執行或繼續使用 **F5** (不建議使用 **F8**，因為在執行指令碼的選取項目時不會評估 $PSScriptRoot)。
* 按一下或選取一行，然後按 **F9** 放置中斷點。
* 使用 **F10** 不進入函式或指令碼呼叫。
* 使用 **F11** 逐步執行函式或指令碼呼叫。
* 跳離 hello 目前函式或指令碼呼叫使用**Shift + F11**。


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>使用 SSMS 瀏覽資料庫結構描述並執行 SQL 查詢

使用[SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect 並瀏覽 hello 應用程式伺服器和資料庫。

hello 部署一開始會有兩個 SQL Database 伺服器 tooconnect 太-hello *tenants1-&lt;使用者&gt;*伺服器和 hello*目錄-&lt;使用者&gt;*伺服器。 tooensure 成功示範連接，這兩部伺服器具有[防火牆規則](sql-database-firewall-configure.md)允許透過所有 Ip。


1. 開啟*SSMS*並連接 toohello *tenants1-&lt;使用者&gt;。.database.windows.net*伺服器。
1. 按一下 [連線] > **[資料庫引擎...]**：

   ![目錄伺服器](media/sql-database-wtp-overview/connect.png)

1. 示範認證︰ 登入= developer、密碼 = P@ssword1

   ![connection](media\sql-database-wtp-overview\tenants1-connect.png)

1. 重複步驟 2-3，並連接 toohello*目錄-&lt;使用者&gt;。.database.windows.net*伺服器。

成功連線之後，您會看到這兩部伺服器。 您的資料庫清單可能會有所不同，您已佈建的 hello 租用戶：

![物件總管](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>後續步驟

[部署 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
