---
title: "使用 SQL 資料庫的多租用戶應用程式的記錄分析 aaaUse |Microsoft 文件"
description: "設定並使用與 hello Azure SQL Database 範例 Wingtip SaaS 應用程式的記錄分析 (OMS)"
keywords: SQL Database Azure
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: billgib; sstein
ms.openlocfilehash: fa9085ce3462939e66853faa2a3cd71e0f6c2581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="setup-and-use-log-analytics-oms-with-hello-wingtip-saas-app"></a>設定並使用與 hello Wingtip SaaS 應用程式的記錄分析 (OMS)

在本教學課程中，您會設定及使用 *Log Analytics([OMS](https://www.microsoft.com/cloud-platform/operations-management-suite))*，以便監視彈性集區和資料庫。 它是在 hello 基礎[效能監視與管理教學課程](sql-database-saas-tutorial-performance-monitoring.md)，並示範如何 toouse*記錄分析*hello Azure 入口網站中提供的 tooaugment hello 監視和警示。 Log Analytics 特別適合用於大規模監視和警示，因為它可支援數百個集區和數十萬個資料庫。 它也提供單一監視解決方案，可以跨多個 Azure 訂用帳戶，整合不同應用程式和 Azure 服務的監視。

在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 安裝及設定 Log Analytics (OMS)
> * 使用記錄分析 toomonitor 集區和資料庫

toocomplete 完成本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)

請參閱 hello[效能監視與管理教學課程](sql-database-saas-tutorial-performance-monitoring.md)hello SaaS 案例和模式，以及它們如何影響 hello 需求上監控解決方案的討論。

## <a name="monitoring-and-managing-performance-with-log-analytics-oms"></a>使用 Log Analytics (OMS) 監視和管理效能

針對 SQL Database，可使用資料庫和集區監視與警示功能。 監視和警示，此內建特定資源且方便的數量不多的資源，但較不適合的 toomonitoring 大型的安裝或在不同的資源和訂用帳戶提供統一的檢視。

對於高容量的情況，可以使用 Log Analytics。 這是不同的 Azure 服務，以提供分析發出診斷記錄檔，可以從許多收集遙測記錄分析工作區中收集的遙測服務與要使用的 tooquery，設定警示。 Log Analytics 可提供內建的查詢語言和資料視覺化工具，以便進行操作資料分析和視覺化。 hello SQL 分析解決方案提供了許多預先定義的彈性集區和資料庫的監視和警示檢視和查詢，並可讓您新增您自己的臨機操作查詢，並視需要儲存這些。 OMS 也提供自訂檢視設計工具。

Hello Azure 入口網站中，在 OMS 中，您可以開啟記錄分析工作區和分析解決方案。 hello Azure 入口網站是 hello 較新存取點，但動作可能落後 hello OMS 入口網站上某些區域中。

### <a name="start-hello-load-generator-toocreate-data-tooanalyze"></a>啟動 hello 負載產生器 toocreate 資料 tooanalyze

1. 開啟**示範 PerformanceMonitoringAndManagement.ps1**在 hello **PowerShell ISE**。 保持此指令碼開啟您可能會想 toorun 幾個 hello 負載產生案例在本教學課程。
1. 如果您有不超過五個租用戶，佈建租用戶 tooprovide 更有趣的監視內容的批次：
   1. 設定 **$DemoScenario = 1**，**佈建一批租用戶**
   1. 按**F5** toorun hello 指令碼。

1. 設定 **$DemoScenario** = 2，**產生一般強度負載 (約為 40 DTU)**。
1. 按**F5** toorun hello 指令碼。

## <a name="get-hello-wingtip-application-scripts"></a>取得 hello Wingtip 應用程式指令碼

hello Wingtip 票證指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 指令碼檔位於 hello[學習模組資料夾](https://github.com/Microsoft/WingtipSaaS/tree/master/Learning%20Modules)。 下載 hello**學習模組**資料夾 tooyour 本機電腦，維護它的資料夾結構。

## <a name="installing-and-configuring-log-analytics-and-hello-azure-sql-analytics-solution"></a>安裝和設定記錄分析 hello Azure SQL 分析解決方案

記錄分析是個別的服務需要 toobe 設定。 Log Analytics 會收集 Log Analytics 工作區中的記錄資料和遙測以及計量。 就像 Azure 中的其他資源一樣，工作區是必須建立的資源。 雖然 hello 工作區不需要 toobe hello 中建立相同的資源群組作為其監視的 hello 應用程式，這通常最有意義 hello。 在 hello 案例中的 hello Wingtip SaaS 應用程式，這可讓 hello 工作區 toobe 輕易刪除與 hello 應用程式只要刪除 hello 資源群組。

1. 開啟...\\學習模組\\效能監視與管理\\記錄分析\\*示範 LogAnalytics.ps1*在 hello **PowerShell ISE**。
1. 按**F5** toorun hello 指令碼。

此時您應該可以開啟的記錄分析 hello Azure 入口網站 （或 hello OMS 入口網站） 中。 需要幾分鐘，讓 hello 記錄分析工作區和 toobecome 可見中收集的遙測 toobe。 將會是較長保留 hello 系統收集資料 hello 更有趣的 hello 經驗 hello。 現在是 toograb 飲料-只是確定 hello 負載產生器仍在執行的好時機 ！


## <a name="use-log-analytics-and-hello-sql-analytics-solution-toomonitor-pools-and-databases"></a>使用記錄分析和 hello SQL 分析方案 toomonitor 集區和資料庫


在此練習中，開啟 記錄分析和 hello OMS 入口網站 toolook 在 hello hello 資料庫和集區所收集的遙測。

1. 瀏覽 toohello [Azure 入口網站](https://portal.azure.com)然後按一下 更多服務，以開啟記錄分析記錄分析搜尋：

   ![開啟 Log Analytics](media/sql-database-saas-tutorial-log-analytics/log-analytics-open.png)

1. 選取名為 hello 工作區*wtploganalytics-&lt;使用者&gt;*。

1. 選取**概觀**tooopen hello hello Azure 入口網站中的記錄分析解決方案。
   ![overview-link](media/sql-database-saas-tutorial-log-analytics/click-overview.png)

    **重要**： 可能需要幾分鐘的時間才能 hello 方案為作用中。 請耐心等候！

1. 按一下 hello Azure SQL 分析磚 tooopen 它。

    ![概觀](media/sql-database-saas-tutorial-log-analytics/overview.png)

    ![分析](media/sql-database-saas-tutorial-log-analytics/analytics.png)

1. hello hello 方案刀鋒視窗中捲動兩側中的檢視與它自己的捲軸在 hello 下方 （重新整理 hello 刀鋒視窗中如有需要）。

1. Hello，即可在它們或個別資源 tooopen 上向下鑽研總管 中，您可以在其中使用中 hello hello 時間滑動軸的各種檢視排名最前面的左邊，或按一下瀏覽垂直列中的 toofocus 上較窄的時間配量。 與此檢視中，您可以選取個別的資料庫或集區 toofocus 特定資源上：

    ![圖表](media/sql-database-saas-tutorial-log-analytics/chart.png)

1. 在 hello 方案刀鋒視窗中，當您捲動 toohello 最右側您會看到一些儲存的查詢，您可以按一下 tooopen，然後瀏覽。 您可以試著修改這些查詢，然後儲存您產生的任何有趣查詢，之後您可重新開啟查詢並使用於其他資源。

1. 在 hello 記錄分析工作區刀鋒視窗中，選取 OMS 入口網站 tooopen hello 方案那里。

    ![oms](media/sql-database-saas-tutorial-log-analytics/oms.png)

1. 在 hello OMS 入口網站，您可以設定警示。 按一下 hello 的 hello 資料庫 DTU 檢視警示的部分。

1. 在 hello 記錄搜尋出現您的檢視，會看到 hello 度量所表示的橫條圖。

    ![log search](media/sql-database-saas-tutorial-log-analytics/log-search.png)

1. 如果您在 [hello] 工具列中按一下警示您將會無法 toosee hello 警示設定，而且可以變更它。

    ![新增警示規則](media/sql-database-saas-tutorial-log-analytics/add-alert.png)

監視和警示記錄分析和 OMS 中的 hello 根據查詢中，透過 hello hello 的工作區中，不同於 hello 每個資源刀鋒視窗中，也就是資源特定的警示。 因此，您可以定義可查看所有資料庫的警示，而不是為每個資料庫定義一個警示。 或是撰寫可使用多種資源類型之複合查詢的警示。 查詢只會受到 hello hello 工作區中可用的資料。

記錄分析的 SQL 資料庫的計費根據 hello hello 工作區中的資料磁碟區。 在此教學課程中，您建立可用的工作區中，這是每日限制的 too500MB。 一旦達到該限制的資料不會再加入 toohello 工作區。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 安裝及設定 Log Analytics (OMS)
> * 使用記錄分析 toomonitor 集區和資料庫

[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)

## <a name="additional-resources"></a>其他資源

* [Hello 初始 Wingtip SaaS 應用程式部署為基礎的其他教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Azure Log Analytics](../log-analytics/log-analytics-azure-sql.md)
* [OMS](https://blogs.technet.microsoft.com/msoms/2017/02/21/azure-sql-analytics-solution-public-preview/)
