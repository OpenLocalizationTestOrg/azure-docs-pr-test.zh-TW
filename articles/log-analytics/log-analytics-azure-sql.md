---
title: "aaaAzure 記錄分析中的 SQL 分析解決方案 |Microsoft 文件"
description: "hello Azure SQL 分析解決方案，可協助您管理 Azure SQL 資料庫。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>使用 Azure SQL Database (預覽) 監視 Log Analytics 中的 Azure SQL Database

![Azure SQL 分析符號](./media/log-analytics-azure-sql/azure-sql-symbol.png)

hello Azure SQL 分析方案中 Azure 記錄分析會收集，並以視覺化方式檢視重要的 SQL Azure 效能度量。 藉由使用 hello 解決方案收集的 hello 度量，您可以建立自訂的監視規則和警示。 而且，您可以跨多個 Azure 訂用帳戶和彈性集區監視 Azure SQL Database 和彈性集區計量，並將其視覺化。 hello 解決方案也可協助您在應用程式堆疊的每個圖層的 tooidentify 問題。  它會使用[Azure 診斷度量](log-analytics-azure-storage.md)一起記錄分析檢視所有您 Azure SQL database 和彈性集區 toopresent 資料單一記錄分析工作區中。

目前，此預覽方案最多可支援 too150 000 Azure SQL Database 和 5000 的 SQL 彈性集區，每個工作區。

hello Azure SQL 分析解決方案，像其他可供記錄分析可協助您監視並收到通知您的 Azure 資源 hello 健全狀況 — 在此情況下，Azure SQL Database。 Microsoft Azure SQL Database 會提供熟悉的 SQL Server 類似功能 tooapplications hello Azure 雲端中執行的可延展的關聯式資料庫服務。 記錄分析可協助您 toocollect、 相互關聯，並將視覺化結構化及未結構化資料。

## <a name="connected-sources"></a>連接的來源

hello Azure SQL 分析解決方案不會使用代理程式 tooconnect toohello 記錄分析服務。

hello 下表描述此解決方案所支援的 hello 連接來源。

| 連接的來源 | 支援 | 說明 |
| --- | --- | --- |
| [Windows 代理程式](log-analytics-windows-agents.md) | 否 | Hello 解決方案不會使用直接的 Windows 代理程式。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否 | Hello 解決方案不會使用直接 Linux 代理程式。 |
| [SCOM 管理群組](log-analytics-om-agents.md) | 否 | 從 hello SCOM 代理程式 tooLog 分析的直接連接不是由 hello 方案。 |
| [Azure 儲存體帳戶](log-analytics-azure-storage.md) | 否 | 記錄分析不會從儲存體帳戶讀取 hello 的資料。 |
| [Azure 診斷](log-analytics-azure-storage.md) | 是 | Azure 的度量資料是直接由 Azure 傳送 tooLog 分析。 |

## <a name="prerequisites"></a>必要條件

- Azure 訂用帳戶。 如果您沒有帳戶，您可以[免費](https://azure.microsoft.com/free/)建立一個。
- Log Analytics 工作區。 您可以使用現有的帳戶，或者您可以在開始使用此解決方案之前[建立一個新的](log-analytics-get-started.md)。
- 啟用 Azure 診斷，您的 Azure SQL database 彈性集區和[設定它們 toosend 其資料 tooLog 分析](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)。

## <a name="configuration"></a>組態

執行下列步驟 tooadd hello Azure SQL 分析方案 tooyour 工作區的 hello。

1. 新增 hello Azure SQL 分析方案 tooyour 從工作區[Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 在 [hello Azure 入口網站，按一下 [**新增**（hello + 符號），然後在 [hello] 清單中的資源，選取**監視 + 管理**。  
    ![監視 + 管理](./media/log-analytics-azure-sql/monitoring-management.png)
3. 在 [hello**監視 + 管理**清單中按一下**查看所有**。
4. 在 hello**建議**清單中，按一下**詳細**，然後在 hello 新清單中，尋找**Azure SQL 分析 （預覽）**並加以選取。  
    ![Azure SQL 分析解決方案](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. 在 [hello **Azure SQL 分析 （預覽）**刀鋒視窗中，按一下 [**建立**。  
    ![建立](./media/log-analytics-azure-sql/portal-create.png)
6. 在 [hello**建立新方案**刀鋒視窗中，選取 hello 工作區中，使用您想 tooadd hello 方案 tooand，然後按一下**建立**。  
    ![新增 tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure 多個 Azure 訂用帳戶

toosupport 多個訂閱，使用中的 hello PowerShell 指令碼[使用 PowerShell 啟用 Azure 資源計量記錄](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)。 從一個 Azure 訂用帳戶 tooa] 工作區中另一個 Azure 訂用帳戶的資源執行 hello 指令碼 toosend 診斷資料時，會當做參數提供 hello 工作區的資源識別碼。

**範例**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>使用 hello 解決方案

當您新增 hello 方案 tooyour 工作區時，hello Azure SQL 分析磚加入 tooyour 工作區中，並出現在 [概觀]。 hello 磚會顯示 hello Azure SQL database 和 hello 方案連接到 Azure SQL 彈性集區數目。

![Azure SQL 分析圖格](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>檢視 Azure SQL 分析資料

按一下 hello **Azure SQL 分析**磚 tooopen hello Azure SQL 分析儀表板。 hello 儀表板包括下列定義 hello 刀鋒視窗。 每個刀鋒視窗會列出 too15 資源 （訂用帳戶、 伺服器、 彈性集區，以及資料庫）。 按一下任何 hello 資源 tooopen hello 儀表板的該特定資源。 彈性集區或資料庫包含 hello 與所選取資源度量的圖表。 按一下圖表 tooopen hello 記錄搜尋] 對話方塊。

| 刀鋒視窗 | 說明 |
|---|---|
| 訂用帳戶 | 具有已連線伺服器、集區及資料庫數目的訂用帳戶清單。 |
| 伺服器 | 具有已連線集區和資料庫數目的伺服器清單。 |
| 彈性集區 | 最大的 GB 和 eDTU 中觀察到的 hello 與已連線的彈性集區的清單期間。 |
|資料庫 | 連接中的資料庫清單與最大 GB DTU hello 觀察到期限。|


### <a name="analyze-data-and-create-alerts"></a>分析資料並建立警示

您可以使用 Azure SQL Database 資源從 hello 資料輕鬆建立警示。 以下是您可用於警示的一些實用[記錄搜尋](log-analytics-log-searches.md)查詢：

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


Azure SQL Database 上的高 DTU

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

Azure SQL Database 彈性集區上的高 DTU

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

您可以使用這些警示為基礎的查詢 tooalert 上特定閾值，Azure SQL Database 和彈性集區。 tooconfigure OMS 工作區的警示：

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure 您的工作區的警示

1. 移 toohello [OMS 入口網站](http://mms.microsoft.com/)並登入。
2. 開啟您已設定為 hello 方案的 hello 工作區。
3. 在 hello 概觀頁面上，按一下 [hello **Azure SQL 分析 （預覽）**磚。
4. 執行的其中一個 hello 範例查詢。
5. 在記錄搜尋中，按一下 [警示]。  
![在搜尋中建立警示](./media/log-analytics-azure-sql/create-alert01.png)
6. 在 [hello**加入警示規則**頁面上，設定 hello 適當的屬性和 hello 特定的臨界值，然後再按一下**儲存**。  
![新增警示規則](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>對 Azure SQL 分析資料採取行動

例如，其中一個 hello 最有用的查詢，您可以執行。 所有 Azure SQL 彈性集區 toocompare hello DTU 使用率在所有 Azure 訂閱 資料庫輸送量單元 (DTU) 提供方式 toodescribe hello Basic、 Standard 和 Premium 資料庫與集區的效能層級的相對容量。 DTU 是根據 CPU、記憶體、讀與寫的混合測量。 當 Dtu 增加時，hello hello 的效能層級提升所提供的電源。 例如，具有 5 個 DTU 的效能層級比具有 1 個 DTU 的效能層級有五倍的能力。 DTU 配額上限，適用於 tooeach 伺服器和彈性集區。

藉由執行 hello 下列記錄搜尋查詢，您可以輕易地分辨您是否未充分使用或超過利用您 SQL Azure 的彈性集區。

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

在下列範例的 hello，您可以看到一個彈性集區具有高使用量接近 100 %dtu 而有些則擁有非常少的使用量。 您可以調查進一步 tootroubleshoot 潛在最近的變更，在您環境中使用 Azure 活動記錄檔。

![記錄搜尋結果 - 高使用率](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>另請參閱

- 使用[記錄搜尋](log-analytics-log-searches.md)記錄分析 tooview 中詳細的 Azure SQL 資料。
- [建立您自己的儀表板](log-analytics-dashboards.md)來顯示 Azure SQL 資料。
- 在特定的 Azure SQL 事件發生時[建立警示](log-analytics-alerts.md)。
