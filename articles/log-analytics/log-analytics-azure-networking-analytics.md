---
title: "aaaAzure 記錄分析中的網路分析解決方案 |Microsoft 文件"
description: "您可以使用 hello 記錄分析 tooreview Azure 網路安全性群組記錄檔及 Azure 應用程式閘道記錄檔中的 Azure 網路分析解決方案。"
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 3674189786bacccc82e6708e78f14c92178e6676
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Log Analytics 中的 Azure 網路監視解決方案

記錄分析會提供下列用於監視您的網路解決方案的 hello:
* 網路效能監視器 (NPM) 以
 * 您的網路監視 hello 健全狀況
* Azure 應用程式閘道分析 tooreview
 * Azure 應用程式閘道記錄檔
 * Azure 應用程式閘道計量
* Azure 網路安全性群組分析 tooreview
 * Azure 網路安全性群組記錄檔

## <a name="network-performance-monitor-npm"></a>網路效能監視器 (NPM)

hello[網路效能監視器](log-analytics-network-performance-monitor.md)管理解決方案是網路監視解決方案，可監視 hello 健全狀況、 可用性和網路的連線。  它是使用的 toomonitor 之間的連線：

* 公用雲端與內部部署環境
* 資料中心與使用者地點 (分公司)
* 裝載多層式應用程式各層的子網路。

如需詳細資訊，請參閱[網路效能監視器](log-analytics-network-performance-monitor.md)。

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure 應用程式閘道和網路安全性群組分析
toouse hello 方案：
1. 新增 hello 管理方案 tooLog 分析，並
2. 啟用診斷 toodirect hello 診斷 tooa 記錄分析工作區。 不需要 toowrite hello 記錄 tooAzure Blob 儲存體。

您可以啟用診斷和 hello 對應之方案的一或兩個應用程式閘道和網路安全性群組。

如果您不要啟用診斷記錄的特定資源類型，但安裝 hello 解決方案，hello 儀表板刀鋒視窗，該資源是空白，並顯示錯誤訊息。

> [!NOTE]
> 在年 1 月 2017 hello 會支援從應用程式閘道和網路安全性群組 tooLog 分析變更傳送記錄檔的方式。 如果您看到 hello **（已過時） 的 Azure 網路分析**方案中，參考太[hello 舊的網路分析解決方案從移轉](#migrating-from-the-old-networking-analytics-solution)步驟中，您需要 toofollow。
>
>

## <a name="review-azure-networking-data-collection-details"></a>檢閱 Azure 網路資料集合詳細資料
hello Azure 應用程式閘道分析與 hello 網路安全性群組分析管理解決方案會直接從 Azure 應用程式閘道和網路安全性群組收集診斷記錄檔。 不必要的 toowrite hello 記錄 tooAzure Blob 儲存體，而且沒有代理程式需要的資料收集。

hello 下表顯示資料收集方法，以及如何針對 Azure 應用程式閘道分析和 hello 網路安全性群組分析收集資料的其他詳細資料。

| 平台 | 直接代理程式 | Systems Center Operations Manager 代理程式 | Azure | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |  |  |&#8226; |  |  |登入時 |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Log Analytics 中的 Azure 應用程式閘道分析解決方案

![Azure 應用程式閘道分析符號](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

應用程式閘道可支援下列記錄檔的 hello:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

應用程式閘道可支援下列度量的 hello:

* 5 分鐘輸送量

### <a name="install-and-configure-hello-solution"></a>安裝和設定 hello 方案
使用下列指示 tooinstall hello，並設定 hello Azure 應用程式閘道分析解決方案：

1. 啟用從 hello Azure 應用程式閘道分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 啟用診斷記錄的 hello[應用程式閘道](../application-gateway/application-gateway-diagnostics.md)想 toomonitor。

#### <a name="enable-azure-application-gateway-diagnostics-in-hello-portal"></a>啟用 hello 入口網站中的 Azure 應用程式閘道診斷

1. 在 [hello Azure 入口網站，瀏覽 toohello 應用程式閘道資源 toomonitor
2. 選取*診斷記錄檔*tooopen hello 遵循頁面

   ![Azure 應用程式閘道資源的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. 按一下*開啟診斷*tooopen hello 遵循頁面

   ![Azure 應用程式閘道資源的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. 診斷，tooturn 按一下*上*下*狀態*
5. 按一下 [hello] 核取方塊*傳送 tooLog 分析*
6. 選取現有的 Log Analytics 工作區，或建立工作區
7. 按一下下方的核取方塊 hello**記錄**hello 記錄類型 toocollect 的每個
8. 按一下*儲存*tooenable hello 記錄診斷 tooLog 分析

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>使用 PowerShell 啟用 Azure 網路診斷

下列 PowerShell 指令碼的 hello 提供的範例 tooenable 應用程式閘道的診斷記錄。

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>使用 Azure 應用程式閘道分析
![Azure 應用程式閘道分析圖格的影像](./media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

按一下 hello 之後**Azure 應用程式閘道分析**磚上 hello 概觀，您可以檢視記錄檔的摘要，而且然後鑽研 toodetails hello 下列類別：

* 應用程式閘道存取記錄檔
  * 應用程式閘道存取記錄檔的用戶端和伺服器錯誤
  * 每個應用程式閘道的每小時要求數
  * 每個應用程式閘道的每小時失敗要求數
  * 應用程式閘道依使用者代理程式分類的錯誤
* 應用程式閘道效能
  * 應用程式閘道的主機健康狀態
  * 應用程式閘道失敗要求的最大和第 95 個百分位數

![Azure 應用程式閘道分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![Azure 應用程式閘道分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-appgateway02.png)

在 [hello **Azure 應用程式閘道分析**儀表板，檢閱其中一個 hello 分頁中的 hello 摘要資訊，然後按一下其中一個 tooview 詳細 hello 記錄搜尋] 頁面上的資訊。

在任何 hello 記錄搜尋] 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。 您也可以篩選由 facet toonarrow hello 結果。


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Log Analytics 中的 Azure 網路安全性群組分析解決方案

![Azure 網路安全性群組分析符號](./media/log-analytics-azure-networking/azure-analytics-symbol.png)

網路安全性群組的相關支援下列記錄檔的 hello:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-hello-solution"></a>安裝和設定 hello 方案
使用下列指示 tooinstall hello 和 hello Azure 網路分析解決方案設定：

1. 啟用從 hello Azure 網路安全性群組分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。
2. 啟用診斷記錄的 hello[網路安全性群組](../virtual-network/virtual-network-nsg-manage-log.md)想 toomonitor 資源。

### <a name="enable-azure-network-security-group-diagnostics-in-hello-portal"></a>Azure 網路安全性群組中啟用診斷 hello 入口網站

1. 在 [hello Azure 入口網站，瀏覽 toohello 網路安全性群組資源 toomonitor
2. 選取*診斷記錄檔*tooopen hello 遵循頁面

   ![Azure 網路安全性群組資源的影像](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. 按一下*開啟診斷*tooopen hello 遵循頁面

   ![Azure 網路安全性群組資源的影像](./media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. 診斷，tooturn 按一下*上*下*狀態*
5. 按一下 [hello] 核取方塊*傳送 tooLog 分析*
6. 選取現有的 Log Analytics 工作區，或建立工作區
7. 按一下下方的核取方塊 hello**記錄**hello 記錄類型 toocollect 的每個
8. 按一下*儲存*tooenable hello 記錄診斷 tooLog 分析

### <a name="enable-azure-network-diagnostics-using-powershell"></a>使用 PowerShell 啟用 Azure 網路診斷

下列 PowerShell 指令碼的 hello 提供的範例 tooenable 的網路安全性群組診斷記錄
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>使用 Azure 網路安全性群組分析
按一下 hello 之後**Azure 網路安全性群組分析**磚上 hello 概觀，您可以檢視記錄檔的摘要，而且然後鑽研 toodetails hello 下列類別：

* 網路安全性群組封鎖流量
  * 網路安全性群組規則與封鎖流量
  * MAC 位址與封鎖流量
* 網路安全性群組允許流量
  * 網路安全性群組規則與允許流量
  * MAC 位址與允許流量

![Azure 網路安全性群組分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-nsg01.png)

![Azure 網路安全性群組分析儀表板的影像](./media/log-analytics-azure-networking/log-analytics-nsg02.png)

在 [hello **Azure 網路安全性群組分析**儀表板，檢閱其中一個 hello 分頁中的 hello 摘要資訊，然後按一下其中一個 tooview 詳細 hello 記錄搜尋] 頁面上的資訊。

在任何 hello 記錄搜尋] 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。 您也可以篩選由 facet toonarrow hello 結果。

## <a name="migrating-from-hello-old-networking-analytics-solution"></a>從 hello 舊的網路分析解決方案移轉
在年 1 月 2017 hello 會支援從 Azure 應用程式閘道和 Azure 網路安全性群組 tooLog 分析變更傳送記錄檔的方式。 這些變更會提供下列優點 hello:
+ 記錄檔寫入直接 tooLog 分析 hello 不需要 toouse 儲存體帳戶
+ 從記錄檔時的 hello 時間延遲越少產生 toothem 可以使用這個記錄分析
+ 較少的組態步驟
+ 所有 Azure 診斷類型的通用格式

toouse hello 更新方案：

1. [設定診斷 toobe 寄件者直接 tooLog 分析 Azure 應用程式閘道](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [設定寄件者直接 tooLog 分析 Azure 網路安全性群組診斷 toobe](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. 啟用 hello *Azure 應用程式閘道分析*和 hello *Azure 網路安全性群組分析*方案使用 hello 程序中所述[中的新增記錄分析解決方案hello 解決方案資源庫](log-analytics-add-solutions.md)
3. 更新任何已儲存的查詢、 儀表板或警示 toouse hello 新的資料類型
  + 類型為 tooAzureDiagnostics。 您可以使用 hello ResourceType toofilter tooAzure 網路記錄檔。

    | 不要使用： | 使用︰ |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |

   + 如有後置字元的任何欄位\_s， \_d 或\_g hello 名稱，變更 hello 第一個字元 toolower 案例中
   + 如有後的置字元的任何欄位\_o 在 [名稱] hello 資料會分成根據 hello 巢狀欄位名稱的個別欄位。
4. 移除 hello *Azure 網路分析 （已過時）*方案。
  + 如果您是使用 PowerShell，請使用 `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that hello workspace is in> -WorkspaceName <name of hello log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`

Hello 新方案中看不到 hello 變更之前，收集資料。 您可以繼續 tooquery，針對使用此資料 hello 舊的類型和欄位名稱。

## <a name="troubleshooting"></a>疑難排解
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 Azure 診斷資料。
