---
title: "aaaDashboards 及瀏覽方式 hello Azure Application Insights |Microsoft 文件"
description: "建立重要 APM 圖表和查詢的檢視。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 39b0701b-2fec-4683-842a-8a19424f67bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 58811388205643bb672e0405b3226f12d0f447a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="navigation-and-dashboards-in-hello-application-insights-portal"></a>瀏覽和 hello Application Insights 入口網站的儀表板
之後[設定您的專案上的 Application Insights](app-insights-overview.md)，您的應用程式效能和使用方式相關的遙測資料會出現在您的專案中 hello 的 Application Insights 資源[Azure 入口網站](https://portal.azure.com)。

## <a name="find-your-telemetry"></a>尋找遙測
登入 toohello [Azure 入口網站](https://portal.azure.com)並瀏覽 toohello 您建立應用程式的 Application Insights 資源。

![按一下 [瀏覽]，選取 [Application Insights]，然後選取您的應用程式。](./media/app-insights-dashboards/00-start.png)

應用程式的 hello 概觀刀鋒視窗 （頁） 顯示 hello 金鑰診斷度量資訊的應用程式的摘要，且閘道 toohello hello 入口網站的其他功能。

![主要路由 tooview 您遙測](./media/app-insights-dashboards/010-oview.png)

您可以自訂任何 hello 圖表和方格，並將其釘選 tooa 儀表板。 這樣一來，您可以匯集 hello 金鑰遙測來自不同的應用程式中央的儀表板上。

## <a name="dashboards"></a>儀表板
hello 首先之後，您看到您登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)是儀表板。 這裡您可以將一起 hello 圖表，在所有的 Azure 資源，包括遙測資料都是最重要的 tooyou [Azure Application Insights](app-insights-overview.md)。

![自訂的儀表板。](./media/app-insights-dashboards/31.png)

1. **瀏覽 toospecific 資源**例如 Application Insights 中的應用程式： 使用 hello 左的工具列。
2. **傳回 toohello 目前儀表板**，或切換 tooother 最近檢視： 使用 hello 下拉式功能表在左上方。
3. **切換儀表板**： 使用 hello 下拉式功能表 hello 儀表板標題
4. **建立、 編輯和共用儀表板**hello 儀表板工具列中。
5. **編輯 hello 儀表板**： 將滑鼠停留在磚，然後使用其上方列 toomove，自訂，或將它移除。

## <a name="add-tooa-dashboard"></a>新增 tooa 儀表板
如果您要尋找在刀鋒視窗或圖表的特別有趣的集合，您可以釘選一份 toohello 儀表板。 您將會在下次返回該處時見到它。

![toopin 圖表中，將滑鼠停留，，然後按一下"…"hello 標頭中。](./media/app-insights-dashboards/33.png)

1. 釘選圖表 toodashboard。 一份 hello 圖表會顯示 hello 儀表板上。
2. Pin hello 整個刀鋒視窗 toohello 儀表板-它會顯示 hello 儀表板上為您可以按一下磚。
3. 按一下 hello 左上的角 tooreturn toohello 目前儀表板。 然後您可以使用 hello 下拉式功能表 tooreturn toohello 目前的檢視。

請注意，圖表會分組為圖格︰一個圖格中可包含多個圖表。 您釘選 hello 整個磚 toohello 儀表板。

hello 圖表會自動重新整理的頻率取決於 hello 圖表的時間範圍：

* 時間範圍向上 too1 小時： 重新整理每隔 5 分鐘
* 介於 1-24 小時的時間範圍：每隔 15 分鐘重新整理一次
* 超過 24 小時的時間範圍：(時間範圍)/60

### <a name="pin-any-query-in-analytics"></a>在分析中釘選任何查詢
您也可以[釘選分析](app-insights-analytics-using.md#pin-to-dashboard)圖表 tooa[共用](#share-dashboards-with-your-team)儀表板。 這可讓您 tooadd 任何任意的查詢，連同 hello 標準度量的圖表。 

系統會每小時自動重新計算結果。 立即按一下 hello 圖表 toorecalculate hello 重新整理圖示。 (瀏覽器重新整理並不會重新計算)。

## <a name="adjust-a-tile-on-hello-dashboard"></a>調整 hello 儀表板上的磚
Hello 儀表板上並排顯示之後，您就可以進行調整。

![將滑鼠停留在圖表中順序 tooedit 它。](./media/app-insights-dashboards/36.png)

1. 新增圖表 toohello 磚。
2. 設定 hello 公制，群組的維度和圖表的樣式 （表格、 圖形）。
3. 拖曳橫跨 hello 圖表 toozoom按一下 hello 復原按鈕 tooreset hello timespan。hello 磚上設定 hello 圖表的篩選屬性。
4. 設定圖格的標題。

從計量瀏覽器刀鋒釘選的圖格，編輯選項會比從 [概觀] 刀鋒視窗釘選的圖格多。

hello 原始您釘選的磚才不會受到您的編輯。

## <a name="switch-between-dashboards"></a>切換儀表板
您可以儲存多個儀表板並在之間進行切換。 當您釘選圖表或刀鋒視窗中時，這些被加入 toohello 目前儀表板。

![tooswitch 之間儀表板，按一下儀表板，然後選取 已儲存的儀表板。 toocreate 並儲存新的儀表板，請按一下 [新增]。 按一下 編輯 toorearrange。](./media/app-insights-dashboards/32.png)

例如，您可能必須以全螢幕顯示 hello 小組室，和另一個用於一般開發中的一個儀表板。

Hello 儀表板，在刀鋒視窗會顯示為圖格： toogo toohello 刀鋒視窗中按一下它。 圖表會複寫其原始位置中的 hello 圖表。

![按一下它所代表的磚 tooopen hello 刀鋒視窗](./media/app-insights-dashboards/35.png)

## <a name="share-dashboards"></a>共用儀表板
建立儀表板之後，您可以與其他使用者共用它。

![在 hello 儀表板標題中，按一下 共用](./media/app-insights-dashboards/41.png)

深入了解 [角色和存取控制](app-insights-resources-roles-access-control.md)。

## <a name="app-navigation"></a>應用程式導覽
hello 概觀刀鋒視窗 hello 閘道 toomore 資訊是有關您的應用程式。

* **任何圖表或圖格**-按一下任何磚或圖表 toosee 有關它會顯示其他詳細資料。

### <a name="overview-blade-buttons"></a>概觀刀鋒視窗按鈕
![概觀刀鋒視窗頂端導覽列](./media/app-insights-dashboards/app-overview-top-nav.png)

* [**計量瀏覽器**](app-insights-metrics-explorer.md) - 建立自己的效能和使用量圖表。
* [**搜尋**](app-insights-diagnostic-search.md) - 調查事件的特定執行個體，例如要求、例外狀況或記錄檔案追蹤。
* [**分析**](app-insights-analytics.md) - 遙測的強大查詢。
* **時間範圍**-調整 hello hello 刀鋒視窗上的所有 hello 圖表所顯示的範圍。
* **刪除**-刪除此應用程式的 hello Application Insights 資源。 您應該也請移除您的應用程式程式碼中的 hello Application Insights 套件或編輯 hello[檢測金鑰](app-insights-create-new-resource.md#copy-the-instrumentation-key)在您的應用程式 toodirect 遙測 tooa 不同 Application Insights 資源。

### <a name="essentials-tab"></a>Essentials 索引標籤
* [檢測金鑰](app-insights-create-new-resource.md#copy-the-instrumentation-key) - 識別此應用程式資源。
* 價格 - 提供功能並設定磁碟區上限。

### <a name="app-navigation-bar"></a>應用程式導覽列
![左導覽列](./media/app-insights-dashboards/app-left-nav-bar.png)

* **概觀**-傳回 toohello 應用程式概觀刀鋒視窗。
* **活動記錄檔** - 警示與 Azure 系統管理事件。
* [**存取控制**](app-insights-resources-roles-access-control.md) -提供存取 tooteam 成員等等。
* [**標記**](../azure-resource-manager/resource-group-using-tags.md) -使用標記 toogroup 與其他應用程式。

調查

* [**應用程式對應**](app-insights-app-map.md) -作用中的地圖顯示 hello 元件的應用程式時，衍生自 hello 相依性資訊。
* [**智慧型偵測**](app-insights-proactive-diagnostics.md) - 檢閱最近的效能警示。
* [**即時串流**](app-insights-live-stream.md) - 一組固定且幾近即時的計量，在部署新組建或偵錯時非常實用。
* [**可用性 / Web 測試**](app-insights-monitor-web-app-availability.md) -傳送一般要求 tooyour web 應用程式從 hello world.* 周圍
* [**失敗、 效能**](app-insights-web-monitor-performance.md) -例外狀況、 失敗率和回應時間要求 tooyour 應用程式和從您的應用程式的要求太[相依性](app-insights-asp-net-dependencies.md)。
* [**效能**](app-insights-web-monitor-performance.md) - 回應時間、相依性回應時間。
* [伺服器](app-insights-web-monitor-performance.md) - 效能計數器。 當您 [安裝狀態監視器](app-insights-monitor-performance-live-website-now.md)時適用。
* **瀏覽器** - 頁面檢視和 AJAX 效能。 當您 [檢測網頁](app-insights-javascript.md)時適用。
* **使用量** - 頁面檢視、使用者和工作階段計數。 當您 [檢測網頁](app-insights-javascript.md)時適用。

設定

* **開始使用** - 內嵌教學課程。
* **屬性** - 檢測金鑰、訂用帳戶和資源識別碼。
* [警示](app-insights-alerts.md) - 計量警示組態。
* [連續匯出](app-insights-export-telemetry.md)-設定匯出的遙測 tooAzure 儲存體。
* [效能測試](app-insights-monitor-web-app-availability.md#performance-tests) - 設定您的網站上的模擬負載。
* [配額和價格](app-insights-pricing.md)和[擷取取樣](app-insights-sampling.md)。
* **應用程式開發介面存取**-建立[版本註解](app-insights-annotations.md)和 hello 資料存取 API。
* [**工作項目**](app-insights-diagnostic-search.md#create-work-item) -連接 tooa 工作追蹤系統，好讓您可以建立 bug 時檢查遙測。

設定

* [**鎖定**](../azure-resource-manager/resource-group-lock-resources.md) -鎖定 Azure 資源
* [**自動化指令碼**](app-insights-powershell.md) -匯出的 hello Azure 資源的定義，以便您可以將它當做範本 toocreate 新資源。


## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a>後續步驟

|  |  |
| --- | --- |
| [計量瀏覽器](app-insights-metrics-explorer.md)<br/>篩選與分割計量 |![搜尋範例](./media/app-insights-dashboards/64.png) |
| [診斷搜尋](app-insights-diagnostic-search.md)<br/>尋找和檢查事件、相關的事件，並建立 Bug |![搜尋範例](./media/app-insights-dashboards/61.png) |
| [分析](app-insights-analytics.md)<br/>功能強大的查詢語言 |![搜尋範例](./media/app-insights-dashboards/63.png) |
