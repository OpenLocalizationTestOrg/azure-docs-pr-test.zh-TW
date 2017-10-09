---
title: "aaaAzure SQL database 的度量 （& s) 診斷記錄 |Microsoft 文件"
description: "瞭解如何設定 Azure SQL Database 資源 toostore 資源使用狀況、 連接及查詢執行統計資料。"
services: sql-database
documentationcenter: 
author: vvasic
manager: jhubbard
editor: 
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: vvasic
ms.openlocfilehash: e6f9e24992ca4f84f701e1ef858e98dc7b481e28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-metrics-and-diagnostics-logging"></a>Azure SQL Database 計量和診斷記錄 
Azure SQL Database 可以發出計量和診斷記錄，以便進行監視。 您可以設定 Azure SQL Database toostore 資源使用狀況、 背景工作工作階段，以及連線至一個 Azure 資源：
- **Azure 儲存體**：用於封存大量遙測資料，價格低廉
- **Azure 事件中樞**：用於整合 Azure SQL Database 遙測與自訂監視解決方案或管線
- **Azure 記錄分析**： 的現成 hello 監視與報告、 警示與緩和功能解決方案 

    ![架構](./media/sql-database-metrics-diag-logging/architecture.png)

## <a name="enable-logging"></a>啟用記錄

預設未啟用計量和診斷記錄功能。 您可以啟用和管理度量和診斷記錄，使用其中一種 hello 下列方法：
- Azure 入口網站
- PowerShell
- Azure CLI
- REST API 
- Resource Manager 範本

當您啟用度量和診斷記錄時，您會需要 toospecify hello Azure 資源收集選取的資料的位置。 可用的選項︰
- Log Analytics
- 事件中樞
- Azure 儲存體 

您可以佈建新的 Azure 資源，或選取現有的資源。 選取後 hello 儲存體資源，您需要 toospecify 哪些資料 toocollect。 可用的選項包括︰

- **[1 分鐘的計量](sql-database-metrics-diag-logging.md#1-minute-metrics)** - 包含 DTU 百分比、DTU 限制、CPU 百分比、實體資料讀取百分比、記錄寫入百分比、成功/失敗/防火牆封鎖的連線、工作階段百分比、背景工作百分比、儲存體、儲存體百分比、XTP 儲存體百分比

如果您指定事件中心] 或 [AzureStorage 帳戶，您可以指定保留原則 toospecify 早於所選時段會刪除該資料。 如果您指定記錄分析，hello 保留原則必須倚賴 hello 選取的定價層。 深入了解 [Log Analytics 價格](https://azure.microsoft.com/pricing/details/log-analytics/)。 

我們建議您先閱讀這兩個 hello[的 Microsoft Azure 中的度量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md)和[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章 toogain 了解不只如何 tooenable 記錄，但 hello度量和記錄檔分類 hello 支援各種 Azure 服務。

### <a name="azure-portal"></a>Azure 入口網站

tooenable 度量 hello Azure 入口網站中的診斷記錄檔集合 tooyour Azure SQL 資料庫或彈性集區 頁面上，瀏覽，然後按一下**診斷設定**。

   ![在 hello Azure 入口網站中啟用](./media/sql-database-metrics-diag-logging/enable-portal.png)

### <a name="powershell"></a>PowerShell

tooenable 度量和記錄診斷使用 PowerShell，使用下列命令的 hello:

- tooenable 儲存體的診斷記錄檔儲存體帳戶，使用此命令：

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
   ```

   儲存體帳戶識別碼 hello 是 hello 資源識別碼 hello 儲存體帳戶 toowhich 想 toosend hello 記錄檔。

- tooenable 串流的診斷記錄檔 tooan 事件中心使用此命令：

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
   ```

   服務匯流排規則識別碼 hello 是這種格式的字串：

   ```powershell
   {service bus resource ID}/authorizationrules/{key name}
   ``` 

- tooenable 傳送的診斷記錄檔 tooa 記錄分析工作區中，使用此命令：

   ```powershell
   Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
   ```

- 您可以取得您記錄分析工作區中使用下列命令的 hello hello 資源識別碼：

   ```powershell
   (Get-AzureRmOperationalInsightsWorkspace).ResourceId
   ```

您可以結合這些參數 tooenable 多個輸出選項。

### <a name="cli"></a>CLI

tooenable 度量和診斷記錄使用 hello Azure CLI，下列命令使用 hello:

- tooenable 儲存體的診斷記錄檔儲存體帳戶，使用此命令：

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
   ```

   儲存體帳戶識別碼 hello 是 hello 資源識別碼 hello 儲存體帳戶 toowhich 想 toosend hello 記錄檔。

- tooenable 串流的診斷記錄檔 tooan 事件中心使用此命令：

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
   ```

   服務匯流排規則識別碼 hello 是這種格式的字串：

   ```azurecli-interactive
   {service bus resource ID}/authorizationrules/{key name}
   ```

- tooenable 傳送的診斷記錄檔 tooa 記錄分析工作區中，使用此命令：

   ```azurecli-interactive
   azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
   ```

您可以結合這些參數 tooenable 多個輸出選項。

### <a name="rest-api"></a>REST API

了解太[變更使用 hello Azure 監視 REST API 的診斷設定](https://msdn.microsoft.com/library/azure/dn931931.aspx)。 

### <a name="resource-manager-template"></a>Resource Manager 範本

了解太[啟用診斷設定，在建立資源時使用資源管理員範本](../monitoring-and-diagnostics/monitoring-enable-diagnostic-logs-using-template.md)。 

## <a name="stream-into-log-analytics"></a>串流到 Log Analytics 中 
Azure SQL Database 標準和診斷的記錄檔可以傳送到記錄分析使用 hello 內建 「 傳送 tooLog 分析 」 選項，在 hello 入口網站或透過 Azure PowerShell cmdlet、 Azure CLI 或 Azure 監視 REST 的診斷設定中啟用記錄分析應用程式開發介面。

### <a name="installation-overview"></a>安裝概觀

透過 Log Analytics 可以輕易監視 Azure SQL Database Fleet。 需要三個步驟：

1.  建立 Log Analytics 資源
2.  將資料庫 toorecord 標準和診斷的記錄檔設定成 hello 建立記錄分析
3.  在 Log Analytics 中從資源庫安裝 **Azure SQL 分析**解決方案

### <a name="create-log-analytics-resource"></a>建立 Log Analytics 資源

1. 按一下**新增**hello 左側功能表中。
2. 按一下 [監視 + 管理]
3. 按一下 [Log Analytics]
4. Hello 記錄分析表單中填入 hello 所需的其他資訊： 工作區名稱、 訂用帳戶、 資源群組、 位置及定價層。

   ![Log Analytics](./media/sql-database-metrics-diag-logging/log-analytics.png)

### <a name="configure-databases-toorecord-metrics-and-diagnostic-logs"></a>設定資料庫 toorecord 標準和診斷的記錄檔

hello 其中資料庫會記錄其度量最簡單方式 tooconfigure 是透過 hello Azure 入口網站。 在 hello Azure 入口網站，瀏覽 tooyour Azure SQL Database 資源，並按一下**診斷設定**。 

### <a name="install-hello-azure-sql-analytics-solution-from-gallery"></a>從組件庫安裝 hello Azure SQL 分析解決方案  

1. 一旦建立 hello 記錄分析資源，且您的資料會流入，Azure SQL 分析方案的安裝。 這可以透過 hello**解決方案資源庫**hello OMS 首頁上和 hello 側邊功能表可以找到。 在 hello 圖庫中，尋找並按一下**Azure SQL 分析**方案，然後按一下**新增**。

   ![監視解決方案](./media/sql-database-metrics-diag-logging/monitoring-solution.png)

2. 您的 OMS 首頁上隨即出現名為 [Azure SQL 分析] 的新圖格。 選取此磚會開啟 hello Azure SQL 分析儀表板。

### <a name="using-azure-sql-analytics-solution"></a>使用 Azure SQL 分析解決方案

Azure SQL 分析是階層式的儀表板，可讓您透過 Azure SQL Database 資源的 hello 階層 toonavigate。 高層級，但它也監視的您 toodo 可讓您 tooscope 此功能可讓您正確監視 toojust hello 設定的資源。
儀表板包含 hello hello 選取資源 下的不同資源的清單。 例如，針對選取的訂閱您所見 hello 選取訂用帳戶的所有伺服器、 彈性集區和 toohello 屬於資料庫。 此外，彈性集區和資料庫，您可以看到該資源的 hello 資源使用量度量。 這包括 DTU、CPU、IO、LOG、工作階段、背景工作、連線和儲存體 (以 GB 為單位) 的圖表。

## <a name="stream-into-azure-event-hub"></a>串流到 Azure 事件中樞中

Azure SQL Database 標準和診斷的記錄檔可以傳送到事件中心使用 hello 內建 「 資料流 tooan 事件中樞 」 選項，在 hello 入口網站或透過 Azure PowerShell Cmdlet、 Azure CLI 或 Azure 監視 REST 的診斷設定中啟用服務匯流排規則識別碼應用程式開發介面。 

### <a name="what-toodo-with-metrics-and-diagnostic-logs-in-event-hub"></a>計量和事件中心中的診斷記錄檔以何種 toodo？
一旦選取 hello 資料流到事件中心時，會是一個進階監視案例的步驟接近 tooenabling。 事件中心做為 hello 「 前端 」 是事件管線，而一旦資料收集到事件中心時，它可以轉換，並儲存使用即時分析的任何提供者或批次處理/儲存體介面卡。 事件中心，讓事件取用者可以存取自己的排程上的 hello 事件，以減少 hello 生產環境的 hello 耗用量的那些事件的事件資料流。 如需事件中樞的詳細資訊，請參閱：

- [Azure 事件中樞是什麼](../event-hubs/event-hubs-what-is-event-hubs.md)？
- [開始使用事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)


以下是幾個方法，您可能會使用資料流功能的 hello:

-   檢視服務健全狀況透過串流處理將 [最忙碌路徑] 資料 tooPowerBI-使用事件中心、 Stream Analytics 中，與 power Bi，您可以輕鬆地將轉換度量和診斷資料接近即時的深入資訊在您的 Azure 服務。 概觀 tooset 向上事件中心，使用 Stream Analytics 中，處理資料，以及使用 power Bi 做為輸出，請參閱[Stream Analytics 與 Power BI](../stream-analytics/stream-analytics-power-bi-dashboard.md)。
-   資料流記錄 toothird 合作對象記錄與遙測資料流 – 使用事件中心的串流處理您可以取得您的診斷記錄檔和度量 toodifferent 第三方監視和記錄檔分析解決方案。 
-   如果您已自訂的遙測平台，或都只考慮的建立一個具有高擴充性 hello 發行-訂閱性質的事件中心可讓您 tooflexibly 擷取診斷記錄檔，請建立自訂遙測及記錄平台。 請參閱[Dan Rosanova 指南 toousing 事件中心全球遙測平台中](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)。

## <a name="stream-into-azure-storage"></a>串流到 Azure 儲存體中

Azure SQL Database 的度量和診斷記錄檔可以儲存到 Azure 儲存體使用 hello 內建 「 封存 tooa 儲存體帳戶 選項，在 hello Azure 入口網站，或藉由啟用 Azure 儲存體透過 Azure PowerShell Cmdlet、 Azure CLI 或 Azure 診斷設定監視 REST API。

### <a name="schema-of-metrics-and-diagnostic-logs-in-hello-storage-account"></a>標準和 hello 儲存體帳戶中的診斷記錄檔的結構描述

在您設定的度量和診斷記錄檔集合，hello hello 第一個資料列的資料可用時，您選取的儲存體帳戶中建立儲存體容器。 這些 blob hello 結構是：

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ databases/{database_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```
    
或者，形式更簡單：

```powershell
insights-{metrics|logs}-{category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

例如，1 分鐘計量的 blob 名稱可能是︰

```powershell
insights-metrics-minute/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.SQL/ servers/Server1/databases/database1/y=2016/m=08/d=22/h=18/m=00/PT1H.json
```

如果您想 toorecord hello hello 彈性集區的資料時，blob 名稱是有點不同：

```powershell
insights-{metrics|logs}-{category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/ RESOURCEGROUPS/{resource group name}/PROVIDERS/Microsoft.SQL/servers/{resource_server}/ elasticPools/{elastic_pool_name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json
```

### <a name="download-metrics-and-logs-from-azure-storage"></a>從 Azure 儲存體下載計量和記錄

請參閱[從 Azure 儲存體下載計量和診斷記錄](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)

## <a name="1-minute-metrics"></a>1 分鐘計量

| |  |
|---|---|
|**Resource**|**計量**|
|資料庫|DTU 百分比、使用的 DTU、DTU 限制、CPU 百分比、實體資料讀取百分比、記錄寫入百分比、成功/失敗/防火牆封鎖的連線、工作階段百分比、背景工作百分比、儲存體、儲存體百分比、XTP 儲存體百分比、死結 |
|彈性集區|eDTU 百分比、使用的 eDTU、eDTU 限制、CPU 百分比、實體資料讀取百分比、記錄寫入百分比、工作階段百分比、背景工作百分比、儲存體、儲存體百分比、儲存體限制、XTP 儲存體百分比 |
|||

## <a name="next-steps"></a>後續步驟

- 讀取這兩個 hello[的 Microsoft Azure 中的度量概觀](../monitoring-and-diagnostics/monitoring-overview-metrics.md)和[概觀的 Azure 診斷記錄檔](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)文章 toogain 了解不只如何 tooenable 記錄，但 hello 度量和記錄類別目錄支援 hello 各種 Azure 服務。
- 閱讀有關事件中心這些文章 toolearn:
   - [Azure 事件中樞是什麼](../event-hubs/event-hubs-what-is-event-hubs.md)？
   - [開始使用事件中樞](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)
- 請參閱[從 Azure 儲存體下載計量和診斷記錄](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs)
