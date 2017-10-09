---
title: "在 OMS 中的健全狀況解決方案 aaaAgent |Microsoft 文件"
description: "本文是預定的 toohelp 您了解如何 toouse 這個方案 toomonitor hello 的健全狀況報告直接 tooOMS 或 System Center Operations Manager 代理程式。"
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>OMS 中的代理程式健全狀況解決方案
在 OMS 中的 hello 代理程式健全狀況解決方案可協助您了解，針對所有 hello 代理程式回報直接 toohello OMS 工作區或 System Center Operations Manager 管理群組連線 tooOMS 」，也就是沒有回應，正在提交作業的資料。  您可以也追蹤的部署代理程式數目，讓它們會分散到各地區，並執行 hello 發佈，部署在 Azure 中，其他雲端環境中或在內部部署的代理程式的其他查詢 toomaintain 感知功能。    

## <a name="prerequisites"></a>必要條件
這個方案部署之前，請確認您有目前支援[Windows 代理程式](../log-analytics/log-analytics-windows-agents.md)reporting toohello OMS 工作區，或報告 tooan [Operations Manager 管理群組](../log-analytics/log-analytics-om-agents.md)整合到您OMS 工作區。    

## <a name="solution-components"></a>方案元件
這個解決方案包含 hello 遵循 tooyour 工作區和直接連接的代理程式或 Operations Manager 連線的管理群組所新增的資源。

### <a name="management-packs"></a>管理組件
如果您的 System Center Operations Manager 管理群組連線的 tooan OMS 工作區，hello 下列管理組件會安裝在 Operations Manager。  新增此解決方案之後，這些管理組件也會安裝在直接連線的 Windows 電腦上。 沒有任何 tooconfigure 或管理這些管理組件。

* Microsoft System Center Advisor HealthAssessment Direct Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor HealthAssessment Server Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentViaServer)。  

如需有關解決方案管理組件的更新方式的詳細資訊，請參閱[Operations Manager 連線 tooLog 分析](../log-analytics/log-analytics-om-agents.md)。

## <a name="configuration"></a>組態
新增使用 hello 程序的 OMS 工作區中所述的 hello 代理程式健全狀況解決方案 tooyour[新增解決方案](../log-analytics/log-analytics-add-solutions.md)。 不需要進一步的組態。


## <a name="data-collection"></a>資料收集
### <a name="supported-agents"></a>支援的代理程式
hello 下表描述此解決方案所支援的 hello 連接來源。

| 連接的來源 | 支援 | 說明 |
| --- | --- | --- |
| Windows 代理程式 | 是 | 系統會從直接 Windows 代理程式收集活動訊號事件。|
| System Center Operations Manager 管理群組 | 是 | 活動訊號事件從代理程式每隔 60 秒 reporting toohello 管理群組收集，然後轉送 tooLog 分析。 從 Operations Manager 代理程式 tooLog 的直接連接分析不需要。 活動訊號的事件資料會轉送 hello 管理群組 toohello 記錄分析儲存機制中。|

## <a name="using-hello-solution"></a>使用 hello 解決方案
當您新增 hello 方案 tooyour OMS 工作區時，hello**代理程式健全狀況**磚加入 tooyour OMS 儀表板。 這個磚會顯示 hello 總數的代理程式和代理程式沒有回應的 hello 數目 hello 在過去 24 小時。<br><br> ![儀表板上的代理程式健全狀況圖格](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

按一下 hello**代理程式健全狀況**磚 tooopen hello**代理程式健全狀況**儀表板。  hello 儀表板會納入 hello 下表中的 hello 資料行。 每個資料行列出 hello 前十個事件所比對資料行的 hello 準則指定的時間範圍內的計數。 您可以執行提供 hello 整個清單，選取 記錄搜尋**查看所有**在 hello 右下的每個資料行，或按一下 hello 資料行標頭。

| 資料欄 | 說明 |
|--------|-------------|
| 不同時間的代理程式計數 | Linux 和 Windows 代理程式為期七天的代理程式計數趨勢。|
| 沒有回應的代理程式計數 | 尚未傳送活動訊號在 hello 過去 24 小時內的代理程式的清單。|
| 依 OS 類型分配 | 劃分您的環境中有多少個 Windows 和 Linux 代理程式。|
| 依代理程式版本分配 | Hello 另一個代理程式版本安裝在您的環境以及每個計數的資料分割。|
| 依代理程式類別分配 | Hello 不同類別的代理程式正在傳送活動訊號事件的資料分割： 直接代理程式 」、 「 OpsMgr 代理程式或 「 hello OpsMgr 管理伺服器。|
| 依管理群組分配 | 您的環境中 hello 不同 SCOM 管理群組的分割區。|
| 代理程式的地理位置 | 您有代理程式和代理程式已安裝在每個國家/地區的 hello 數目總計數 hello 不同國家/地區的資料分割。|
| 已安裝的閘道計數 | hello 具有 hello OMS 閘道安裝，以及一份這些伺服器的伺服器數目。|

![代理程式健全狀況儀表板範例](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Log Analytics 記錄
hello 方案 hello OMS 儲存機制中建立一種類型的記錄。  

### <a name="heartbeat-records"></a>活動訊號記錄
系統會建立類型為 [活動訊號] 的記錄。  這些記錄 hello 下表中都有 hello 屬性。  

| 屬性 | 說明 |
| --- | --- |
| 類型 | *活動訊號*|
| 類別 | 值為 [直接代理程式]、[SCOM 代理程式] 或 [SCOM 管理伺服器]。|
| 電腦 | 電腦名稱。|
| OSType | Windows 或 Linux 作業系統。|
| OSMajorVersion | 作業系統主要版本。|
| OSMinorVersion | 作業系統次要版本。|
| 版本 | OMS 代理程式或 Operations Manager 代理程式版本。|
| SCAgentChannel | 值為 [Direct] 和/或 [SCManagementServer]。|
| IsGatewayInstalled | 如果已安裝 OMS 閘道，值為 true，否則值為 false。|
| ComputerIP | Hello 電腦的 IP 位址。|
| RemoteIPCountry | 電腦部署所在的地理位置。|
| ManagementGroupName | Operations Manager 管理群組的名稱。|
| SourceComputerId | 電腦的唯一識別碼。|
| RemoteIPLongitude | 電腦的地理位置經度。|
| RemoteIPLatitude | 電腦的地理位置緯度。|

報告 tooan Operations Manager 管理伺服器會傳送兩個活動訊號，和 SCAgentChannel 屬性的值將同時包含每個代理程式**直接**和**SCManagementServer**視內容而定記錄分析資料來源，您已啟用您的 OMS 訂用帳戶中的方案。 如果您還記得，解決方案的資料會傳送直接從 Operations Manager 管理伺服器 toohello OMS web 服務，或是因為 hello hello 代理程式上收集而來的資料數量會直接從 hello 代理程式 tooOMS web 服務傳送。 Hello 值的活動訊號事件**SCManagementServer**，hello ComputerIP 值是 hello hello 管理伺服器的 IP 位址，因為 hello 資料實際上上傳它。  活動訊號 SCAgentChannel 設有太**直接**，它是 hello 代理程式的 hello 公用 IP 位址。  

## <a name="sample-log-searches"></a>記錄檔搜尋範例
hello 下表提供範例記錄檔搜尋此解決方案所收集的記錄。

| 查詢 | 說明 |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |代理程式總數 |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |在 hello 過去 24 小時內沒有回應的代理程式的計數 |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |在 hello 過去 15 分鐘內沒有回應的代理程式的計數 |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |電腦線上 （hello 過去 24 小時) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |總代理程式離線在過去 30 分鐘的時間 （hello 過去 24 小時) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |依 OSType 取得一段時間內的代理程式數目趨勢|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |依 OS 類型分配 |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |依代理程式版本分配 |
| Type=Heartbeat&#124;measure count() by Category |依代理程式類別分配 |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | 依管理群組分配 |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |代理程式的地理位置 |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |已安裝的 OMS 閘道數目 |


>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](../log-analytics/log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。
>
>| 查詢 | 說明 |
|:---|:---|
| Heartbeat &#124; distinct Computer |代理程式總數 |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |在 hello 過去 24 小時內沒有回應的代理程式的計數 |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |在 hello 過去 15 分鐘內沒有回應的代理程式的計數 |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |電腦線上 （hello 過去 24 小時) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |總代理程式離線在過去 30 分鐘的時間 （hello 過去 24 小時) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |依 OSType 取得一段時間內的代理程式數目趨勢|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |依 OS 類型分配 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |依代理程式版本分配 |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |依代理程式類別分配 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | 依管理群組分配 |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |代理程式的地理位置 |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |已安裝的 OMS 閘道數目 |

## <a name="next-steps"></a>後續步驟

* 如需有關從 Log Analytics 產生的警示的詳細資料，請深入了解 [Log Analytics 中的警示](../log-analytics/log-analytics-alerts.md) 。
