---
title: "跨多個 Azure SQL database aaaRun 臨機操作分析查詢 |Microsoft 文件"
description: "跨多個 hello Wingtip SaaS 多租用戶應用程式中的 SQL 資料庫執行特定分析查詢。"
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
ms.date: 06/23/2017
ms.author: billgib; sstein
ms.openlocfilehash: 140cd51fdd03b5a548147282b51ceb0ad80c944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-ad-hoc-analytics-queries-across-all-wingtip-saas-tenants"></a>對所有 Wingtip SaaS 租用戶執行臨機操作分析查詢

在本教學課程中，您執行分散式的查詢 hello 整個租用戶資料庫集合 tooenable 臨機操作分析。 彈性查詢是使用的 tooenable 分散式查詢，這需要部署額外的分析資料庫 （toohello 類別目錄伺服器）。 這些查詢可以擷取埋藏在 hello 日常操作的資料的 hello Wingtip SaaS 應用程式的深入資訊。


您會在本教學課程中學到：

> [!div class="checklist"]

> * 有關每個資料庫中的 hello 全域檢視，可讓在租用戶之間的有效率查詢
> * 如何 toodeploy 臨機操作分析資料庫
> * Toorun 如何跨所有租用戶資料庫分散式查詢



toocomplete 完成本教學課程，請確定 hello 下列必要條件：

* hello Wingtip SaaS 應用程式部署。 toodeploy 在五分鐘內，請參閱[部署及瀏覽 hello Wingtip SaaS 應用程式](sql-database-saas-tutorial.md)
* 已安裝 Azure PowerShell。 如需詳細資料，請參閱[開始使用 Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)
* 已安裝 SQL Server Management Studio (SSMS)。 toodownload 並安裝 SSMS，請參閱[下載 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。


## <a name="ad-hoc-analytics-pattern"></a>臨機操作分析模式

Toouse hello 大量集中儲存在 hello 雲端中的租用戶資料的其中一個 hello 與 SaaS 應用程式的絕佳機會。 使用此資料 toogain 深入了解 hello 作業和使用您的應用程式、 您的租用戶、 使用者、 喜好設定、 行為、 等等。這些深入解析可以引導應用程式和服務中的功能開發、使用性改進及其他投資。

在單一多租用戶資料庫中存取此資料很容易，但資料大規模分散於可能數千個資料庫時則不太容易存取。 其中一個方法是 toouse[彈性查詢](sql-database-elastic-query-overview.md)，可讓在一組具有通用的結構描述的資料庫的分散式查詢。 彈性查詢會使用單一*head*外部資料表定義之鏡像資料表或檢視表中 hello 分散式 （租用戶） 資料庫的資料庫。 Toothis 前端資料庫提交的查詢會編譯的 tooproduce 分散式的查詢計劃，與 hello 查詢推 toohello 租用戶資料庫所需的部分。 彈性查詢會使用 hello 分區對應中 hello 類別目錄資料庫 tooprovide hello hello 租用戶資料庫位置。 安裝程式和查詢會直接使用標準 [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference)，以及支援從 Power BI 和 Excel 等工具進行臨機操作查詢。

將查詢分散到 hello 租用戶資料庫，彈性查詢提供立即深入了解即時的實際執行資料。 不過，當彈性查詢會從提取資料可能有多個資料庫，查詢延遲有時可能會高於對等查詢送出 tooa 單一多租用戶資料庫。 設計查詢所傳回的 toominimize hello 資料時請務必小心。 彈性查詢通常最適合查詢的即時資料，少量為相對於的 toobuilding 常用或複雜的分析查詢或報告。 如果查詢不佳，請查看 hello[執行計劃](https://docs.microsoft.com/sql/relational-databases/performance/display-an-actual-execution-plan)toosee hello 查詢的哪個部分已經按向下 toohello 遠端資料庫，然後傳回多少資料。 需要複雜分析處理的查詢，在某些情況下透過將租用戶資料擷取到針對分析查詢最佳化的專用資料庫或資料倉儲來提供服務，可能會比較好。 此模式會說明在 hello[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)。 

## <a name="get-hello-wingtip-application-scripts"></a>取得 hello Wingtip 應用程式指令碼

hello Wingtip SaaS 指令碼和應用程式的原始程式碼中可用 hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github 儲存機制。 [步驟 toodownload hello Wingtip SaaS 指令碼](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts)。

## <a name="create-ticket-sales-data"></a>建立票證銷售資料

toorun 查詢更有趣的資料集，針對執行 hello 票證產生器建立票證的銷售資料。

1. 在 hello *PowerShell ISE*，開啟 hello...\\學習模組\\作業分析\\臨機操作分析\\*示範 AdhocAnalytics.ps1*指令碼，然後設定下列值的 hello:
   * **$DemoScenario** = 1，**購買各地事件的票證**。
2. 按**F5**執行 hello 指令碼，並產生票證銷售。 Hello 指令碼執行時，繼續 hello 步驟在本教學課程。 hello 票券資料會查詢在 hello*執行特定分散式查詢*區段中，因此會等候 hello 票證產生器 toocomplete 時仍在執行時取得 toothat 練習。

## <a name="explore-hello-global-views"></a>瀏覽 hello 全域檢視

hello Wingtip SaaS 應用程式是使用租用戶每個資料庫模型，因此 hello 租用戶資料庫結構描述會定義以單一租用戶的觀點所建立。 租用戶特定資訊位於一個 *Venue* 資料表中，該資料表一律有單一資料列，且會實作成一個沒有主索引鍵的堆積。 Hello 結構描述中的其他資料表不需要 toobe 相關 toohello*法院*資料表，因為在正常使用，都不會租用戶 hello 資料屬於任何不確定。

不過，當跨所有資料庫查詢，務必彈性查詢可以處理 hello 資料，如同它是單一邏輯資料庫分區化依租用戶的一部分。 tooachieve 'global' 的檢視集，這是加入的 toohello 租用戶資料庫專案的全域查詢的 hello 資料表的每個租用戶識別碼。 例如，hello *VenueEvents*檢視新增計算*VenueId* toohello 資料行投射從 hello*事件*資料表。 藉由定義透過 hello 外部資料庫資料表中 hello 前端*VenueEvents* (而不是基礎 hello*事件*資料表)，彈性查詢是根據聯結下的能 toopush *VenueId*讓它們可以平行執行的每個遠端的資料庫 （而不是在 hello 前端資料庫）。 這將可大幅減少 hello 傳回，則會導致許多查詢的效能大幅增加的資料量。 這些全域檢視已在所有租用戶資料庫 (以及在*basetenantdb*) 中預先建立。

1. 開啟 SSMS 和[連接 toohello tenants1-&lt;使用者&gt;伺服器](sql-database-wtp-overview.md#explore-database-schema-and-execute-sql-queries-using-ssms)。
2. 展開 [資料庫]，以滑鼠右鍵按一下 **contosoconcerthall**，然後選取 [新增查詢]。
3. 執行下列查詢 tooexplore hello hello 單一租用戶資料表與差異 hello 全域檢視 hello:

   ```T-SQL
   -- hello base Venue table, that has no VenueId associated.
   SELECT * FROM Venue

   -- Notice hello plural name 'Venues'. This view projects a VenueId column.
   SELECT * FROM Venues

   -- hello base Events table, which has no VenueId column.
   SELECT * FROM Events

   -- This view projects hello VenueId retrieved from hello Venues table.
   SELECT * FROM VenueEvents
   ```

在這些檢視中，hello *VenueId*計算 hello 地點名稱，而任何方法的雜湊為無法使用的 toointroduce 唯一值。 這個方法是 hello 租用戶金鑰計算用於 hello 目錄中的類似 toohello 方法。

hello tooexamine hello 定義*管道*檢視：

1. 在 [物件總管] 中，展開 [contosoconcethall] > [檢視]：

   ![檢視](media/sql-database-saas-tutorial-adhoc-analytics/views.png)

2. 以滑鼠右鍵按一下 **dbo.Venues**。
3. 選取 [指令碼檢視] > [CREATE To] > [新的查詢編輯器視窗]

指令碼的任何其他 hello*法院*檢視 toosee 它們如何新增 hello *VenueId*。

## <a name="deploy-hello-database-used-for-ad-hoc-distributed-queries"></a>部署用來進行特定分散式查詢的 hello 資料庫

此練習將部署的 hello *adhocanalytics*資料庫。 這是 hello 的前端資料庫將會包含用來查詢所有租用戶資料庫之間的 hello 結構描述。 現有的類別目錄伺服器，就是用於所有與管理相關的資料庫，hello 範例應用程式中的 hello 伺服器部署的 toohello hello 資料庫。

1. 開啟...\\學習模組\\作業分析\\臨機操作分析\\*示範 AdhocAnalytics.ps1*在 hello *PowerShell ISE*和集 hello下列值：
   * **$DemoScenario** = 2，**部署臨機操作分析資料庫**。

2. 按**F5** toorun hello 指令碼，並建立 hello *adhocanalytics*資料庫。

Hello 下一節，您會加入結構描述 toohello 資料庫，以便能夠使用的 toorun 分散式查詢。

## <a name="configure-hello-database-for-running-distributed-queries"></a>設定 hello 資料庫以執行分散式的查詢

此練習將結構描述 （hello 外部資料來源和外部資料表定義） toohello 臨機操作分析的資料庫，可讓您跨所有租用戶資料庫查詢。

1. 開啟 SQL Server Management Studio，並連接 toohello hello 先前步驟中建立臨機操作分析資料庫。 hello hello 資料庫名稱會是 adhocanalytics。
2. 在 SSMS 中開啟 ...\Learning Modules\Operational Analytics\Adhoc Analytics\ *Initialize-AdhocAnalyticsDB.sql*。
3. 檢閱 hello SQL 指令碼，並請注意下列 hello:

   彈性查詢會使用資料庫範圍認證 tooaccess 每個的 hello 租用戶資料庫。 這個認證需要 toobe hello 的所有資料庫中可用以及應該通常被授與 hello 最低權限所需 tooenable 這些臨機操作查詢。

    ![建立認證](media/sql-database-saas-tutorial-adhoc-analytics/create-credential.png)

   hello 外部資料來源被定義 toouse hello 租用戶分區對應 hello 類別目錄資料庫中。 使用此選項為 hello 外部資料來源，查詢是分散式的 tooall hello 查詢執行時，在 hello 目錄中註冊的資料庫。 因為每個部署不同的伺服器名稱，此初始化指令碼會藉由擷取 hello 目前的伺服器取得 hello 類別目錄資料庫 hello 位置 (@@servername) hello 指令碼執行的所在。

    ![建立外部資料來源](media/sql-database-saas-tutorial-adhoc-analytics/create-external-data-source.png)

   hello 參考 hello 全域檢視 hello 上一節中所述，以定義外部資料表**發佈 = SHARDED(VenueId)**。 因為每個*VenueId*對應 tooa 單一資料庫，這可改善效能，許多情況下的，hello 下一節中所示。

    ![建立外部資料表](media/sql-database-saas-tutorial-adhoc-analytics/external-tables.png)

   hello 本機資料表*VenueTypes* ，會建立並填入。 此參考資料表是在所有租用戶資料庫中，常見的因此可以表示為本機資料表並填入 hello 一般資料。 這可能會降低 hello 某些查詢的資料量之間移動 hello 租用戶資料庫以及 hello *adhocanalytics*資料庫。

    ![建立資料表](media/sql-database-saas-tutorial-adhoc-analytics/create-table.png)

   如果您以這種方式包含參考資料表，是確定 tooupdate hello 資料表結構描述和資料，每當您更新 hello 租用戶資料庫。

4. 按**F5** toorun hello 指令碼，並初始化 hello *adhocanalytics*資料庫。 

現在您可以執行分散式查詢，然後收集所有租用戶之間的深入資訊！

## <a name="run-ad-hoc-distributed-queries"></a>執行臨機操作分散式查詢

現在該 hello *adhocanalytics*資料庫設定，請繼續並執行一些分散式的查詢。 包括 hello 執行計畫更深入了解 hello 查詢處理發生的位置。 

檢查時 hello 執行計劃，將滑鼠停留在 hello 計劃圖示，以取得詳細資料。 

重要 toonote，為該設定**發佈 = SHARDED(VenueId)**我們定義 hello 外部資料來源，可改善效能，許多案例。 因為每個*VenueId*對應 tooa 單一資料庫中，篩選是我們所需的完成輕鬆地從遠端、 傳回唯一 hello 資料。

1. 在 SSMS 中開啟 ...\\Learning Modules\\Operational Analytics\\Adhoc Analytics\\Demo-AdhocAnalyticsQueries.sql。
2. 確保您已連線的 toohello **adhocanalytics**資料庫。
3. 選取 hello**查詢**功能表，然後按一下**包括實際執行計畫**
4. 反白顯示 hello*目前已註冊的管道？*查詢，然後按**F5**。

   hello 查詢會傳回 hello 整個地點清單，說明如何快速而且容易 tooquery 整個所有租用戶和每個租用戶傳回的資料。

   檢查 hello 計劃，請參閱 hello 整個成本是 hello 遠端查詢，因為我們只是進行 tooeach 租用戶資料庫，然後選取 hello 法院資訊。

   ![SELECT * FROM dbo.Venues](media/sql-database-saas-tutorial-adhoc-analytics/query1-plan.png)

5. 選取 hello 下一個查詢，然後按**F5**。

   此查詢會聯結資料 hello 租用戶資料庫和 hello 本機*VenueTypes*資料表 (本機，因為它是資料表中 hello *adhocanalytics*資料庫)。

   檢查 hello 計劃，並查看該 hello 大部分的成本是 hello 遠端查詢，因為我們查詢每個租用戶法院資訊 (dbo。管道），然後執行快速的本機聯結與 hello 本機*VenueTypes*資料表 toodisplay hello 易記名稱。

   ![遠端資料與本機資料的聯結](media/sql-database-saas-tutorial-adhoc-analytics/query2-plan.png)

6. 現在選取 hello*哪一天是 hello 販售的大部分票證？*查詢，然後按**F5**。

   此查詢會執行比較複雜的聯結和彙總。 什麼是重要的 toonote 是遠端電腦上，完成大部分的 hello 處理，同樣地，我們會傳回唯一 hello 列我們需要傳回只每天每個地點的彙總的票證銷售計數的單一資料列。

   ![query](media/sql-database-saas-tutorial-adhoc-analytics/query3-plan.png)


## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]

> * 對所有租用戶資料庫執行分散式查詢
> * 部署特定分析資料庫，並加入 tooit toorun 分散式查詢的結構描述。


現在，請嘗試 hello[租用戶分析教學課程](sql-database-saas-tutorial-tenant-analytics.md)tooexplore 擷取資料 tooa 個別分析資料庫以進行更複雜的分析處理...

## <a name="additional-resources"></a>其他資源

* 其他[hello Wingtip SaaS 應用程式為基礎的教學課程](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [彈性查詢](sql-database-elastic-query-overview.md)
