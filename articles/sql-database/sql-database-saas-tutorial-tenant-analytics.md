---
title: "針對多個 Azure SQL database aaaRun 分析查詢 |Microsoft 文件"
description: "從租用戶資料庫將資料擷取至分析資料庫，以便進行離線分析"
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
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a>從租用戶資料庫將資料擷取至分析資料庫，以便進行離線分析

在本教學課程中，您使用彈性的工作 toorun 查詢的每個租用戶資料庫。 hello 作業會擷取票證銷售資料，並將其載入至分析資料庫 （或資料倉儲） 中進行分析。 hello 分析資料庫是然後查詢 tooextract 所有租用戶此日常操作資料的深入資訊。


在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 建立 hello 租用戶分析資料庫
> * 建立排程的工作 tooretrieve 資料並填入 hello 分析資料庫

toocomplete 符合本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* 已安裝最新版本的 SQL Server Management Studio (SSMS) hello。 [下載並安裝 SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a>租用戶操作分析模式

Toouse hello 豐富的租用戶資料儲存在 hello 雲端的其中一個 hello 與 SaaS 應用程式的絕佳機會。 使用此資料 toogain 深入了解 hello 作業和您的應用程式和您的租用戶的使用方式。 此資料可以引導開發功能、 使用性增強功能和其他的投資，在 hello 應用程式和平台。 在單一多租用戶資料庫中存取此資料很容易，但資料大規模分散於可能數千個資料庫時則不太容易存取。 一種方法 tooaccessing 這份資料是 toouse 彈性作業，可讓工作執行 toobe 輸出資料庫和資料表中擷取結果傳回查詢結果。

## <a name="get-hello-wingtip-application-scripts"></a>取得 hello Wingtip 應用程式指令碼

hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 [步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。

## <a name="deploy-a-database-for-tenant-analytics-results"></a>部署租用戶分析結果的資料庫

本教學課程需要的 toohave 資料庫部署的 toocapture hello 產生的指令碼，包含傳回結果的查詢執行的作業。 讓我們針對此目的，建立一個稱為 tenantanalytics 的資料庫。

1. 開啟...\\學習模組\\作業分析\\租用戶分析\\*示範 TenantAnalyticsDB.ps1*在 hello *PowerShell ISE*和設定hello 下列值：
   * **$DemoScenario** = **2** *部署操作分析資料庫*
1. 按**F5** toorun hello 的示範指令碼 (該呼叫 hello*部署 TenantAnalyticsDB.ps1*指令碼) 以建立 hello 租用戶分析資料庫。

## <a name="create-some-data-for-hello-demo"></a>建立 hello 示範的某些資料

1. 開啟...\\學習模組\\作業分析\\租用戶分析\\*示範 TenantAnalyticsDB.ps1*在 hello *PowerShell ISE*和設定hello 下列值：
   * **$DemoScenario** = **1** *購買各地事件的票證*
1. 按**F5** toorun hello 指令碼，並建立購買記錄的票證。


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a>建立票證購買項目有關的排程的工作 tooretrieve 租用戶分析

此指令碼會從所有租用戶建立作業 tooretrieve 票證購買資訊。 一旦彙總成單一資料表，您可以取得有關購買模式在 hello 租用戶之間的票證豐富具洞察力的度量。

1. 開啟 SSMS 並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器
1. 開啟 ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\TicketPurchasesfromAllTenants.sql
1. 修改&lt;使用者&gt;，使用 hello 使用者名稱，而您在 hello hello 指令碼頂端，hello Wingtip SaaS 應用程式部署時使用**sp\_新增\_目標\_群組\_成員**和**sp\_新增\_作業步驟**
1. 以滑鼠右鍵按一下，然後選取**連接**，並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器，如果尚未連接
1. 確保您已連線的 toohello **jobaccount**資料庫，然後按**F5**執行 hello 指令碼

* **預存程序\_新增\_目標\_群組**建立 hello 目標群組名稱*TenantGroup*，現在我們需要 tooadd 目標成員。
* **預存程序\_新增\_目標\_群組\_成員**新增*伺服器*目標成員類型，認為 （這是 hello customer1-請注意該伺服器內的所有資料庫&lt;使用者&gt;包含 hello 租用戶資料庫伺服器) 在工作時間執行應該包含在 hello 作業。
* **sp\_add\_job** 會建立新的每週排定作業，其名稱為「所有租用戶的票證購買」
* **預存程序\_新增\_jobstep**從所有租用戶和複製 hello 傳回的結果集至名為的資料表建立 hello 作業步驟包含 T-SQL 命令文字 tooretrieve 所有 hello 票證購買資訊*AllTicketsPurchasesfromAllTenants*
* hello 指令碼中的 hello 剩餘檢視會顯示 hello hello 物件和執行監視作業存在。 檢閱從 hello hello 狀態值**生命週期**資料行 toomonitor hello 狀態。 一次成功，hello 工作已順利完成所有租用戶資料庫上且 hello 包含 hello 的兩個其他資料庫參考資料表。

已成功執行 hello 指令碼，應該會產生類似的結果：

![results](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a>建立從所有租用戶購買票證摘要計數工作 tooretrieve

此指令碼會從所有租用戶建立作業的所有票證購買 tooretrieve 總和。

1. 開啟 SSMS 並連接 toohello*目錄-&lt;使用者&gt;。.database.windows.net*伺服器
1. 開啟 hello 檔案...\\學習模組\\佈建和類別目錄\\作業分析\\租用戶分析\\*結果 TicketPurchasesfromAllTenants.sql*
1. 修改&lt;使用者&gt;，使用 hello 使用者名稱，而當您在 hello 指令碼在 hello hello Wingtip SaaS 應用程式部署時，使用**sp\_新增\_jobstep**預存程序
1. 以滑鼠右鍵按一下，然後選取**連接**，並連接 toohello 目錄-&lt;使用者&gt;。.database.windows.net 伺服器，如果尚未連接
1. 確保您已連線的 toohello **tenantanalytics**資料庫，然後按**F5**執行 hello 指令碼

已成功執行 hello 指令碼，應該會產生類似的結果：

![results](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* **sp\_add\_job** 會建立新的每週排定作業，其名稱為 “ResultsTicketsOrders”

* **預存程序\_新增\_jobstep**從所有租用戶和複製 hello 傳回的結果集至名為 CountofTicketOrders 的資料表建立 hello 作業步驟包含 T-SQL 命令文字 tooretrieve 所有 hello 票證購買資訊

* hello 指令碼中的 hello 剩餘檢視會顯示 hello hello 物件和執行監視作業存在。 檢閱從 hello hello 狀態值**生命週期**資料行 toomonitor hello 狀態。 一次成功，hello 工作已順利完成所有租用戶資料庫上且 hello 包含 hello 的兩個其他資料庫參考資料表。


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 部署租用戶分析資料庫
> * 在租用戶之間建立排程的工作 tooretrieve 分析資料

恭喜！

## <a name="additional-resources"></a>其他資源

* 其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [彈性作業](sql-database-elastic-jobs-overview.md)
