---
title: "aaaAlert 管理解決方案中 Operations Management Suite (OMS) |Microsoft 文件"
description: "hello 警示管理解決方案中記錄分析可協助您分析所有的環境中的 hello 警示。  在加法 tooconsolidating 產生警示，在 OMS 中，它匯入警示連接 System Center Operations Manager 管理群組的記錄分析。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Operations Management Suite (OMS) 中的警示管理解決方案

![Alert Management icon](media/log-analytics-solution-alert-management/icon.png)

hello 警示管理解決方案可協助您分析所有在您的記錄分析儲存機制中的 hello 警示。  這些警示可能來自各種來源，包括[由 Log Analytics 所建立](log-analytics-alerts.md)或[從 Nagios 或 Zabbix 匯入](log-analytics-linux-agents.md)的來源。  hello 解決方案也會匯入警示從任何[已連接 System Center Operations Manager 管理群組](log-analytics-om-agents.md)。

## <a name="prerequisites"></a>必要條件
hello 方案適用於類型為 hello 記錄分析儲存機制中的任何記錄**警示**，因此您必須執行任何設定是必要的 toocollect 這些記錄。

- 記錄分析警示[建立警示規則](log-analytics-alerts.md)toocreate 直接在 hello 儲存機制中的警示記錄。
- Nagios 和 Zabbix 的警示，[設定這些伺服器](log-analytics-linux-agents.md)toosend 警示 tooLog 分析。
- System Center Operations Manager 警示的[連接您 Operations Manager 管理群組 tooyour 記錄分析工作區](log-analytics-om-agents.md)。  在 System Center Operations Manager 中建立的任何警示會匯入至記錄分析。  

## <a name="configuration"></a>組態
新增使用 hello 程序的 OMS 工作區中所述的 hello 警示管理解決方案 tooyour[新增解決方案](log-analytics-add-solutions.md)。  不需要進一步的組態。

## <a name="management-packs"></a>管理組件
如果您的 System Center Operations Manager 管理群組連線的 tooyour OMS 工作區，然後 hello 下列管理組件會安裝在 System Center Operations Manager 時將方案加入。  沒有任何設定或維護 hello 所需的管理組件。  

* Microsoft System Center Advisor 警示管理 (Microsoft.IntelligencePacks.AlertManagement)

如需有關解決方案管理組件的更新方式的詳細資訊，請參閱[Operations Manager 連線 tooLog 分析](log-analytics-om-agents.md)。

## <a name="data-collection"></a>資料收集
### <a name="agents"></a>代理程式
hello 下表描述此解決方案所支援的 hello 連接來源。

| 連接的來源 | 支援 | 說明 |
|:--- |:--- |:--- |
| [Windows 代理程式](log-analytics-windows-agents.md) | 否 |直接的 Windows 代理程式不會產生警示。  您可以從收集自 Windows 代理程式的事件和效能資料建立 Log Analytics 警示。 |
| [Linux 代理程式](log-analytics-linux-agents.md) | 否 |直接的 Linux 代理程式不會產生警示。  您可以從收集自 Linux 代理程式的事件和效能資料建立 Log Analytics 警示。  從這些伺服器需要 hello Linux 代理程式收集 Nagios 和 Zabbix 的警示。 |
| [System Center Operations Manager 管理群組](log-analytics-om-agents.md) |是 |Operations Manager 代理程式產生的警示會傳遞 toohello 管理群組，接著再轉寄 tooLog 分析。<br><br>從 Operations Manager 代理程式 tooLog 的直接連接分析不需要。 警示資料轉送 hello 管理群組 toohello 記錄分析儲存機制中。 |


### <a name="collection-frequency"></a>收集頻率
- 警示記錄是可用 toohello 解決方案，因為它們存放在 hello 儲存機制。
- 每隔三分鐘時，會從 hello Operations Manager 管理群組 tooLog 分析傳送警示的資料。  

## <a name="using-hello-solution"></a>使用 hello 解決方案
當您新增 hello 警示管理解決方案 tooyour OMS 工作區時，hello**警示管理**tooyour OMS 儀表板的磚加入。  這個磚會顯示計數和過去 24 小時內 hello 所產生的目前作用中警示的 hello 數目的圖形表示。  您無法變更此時間範圍。

![Alert Management tile](media/log-analytics-solution-alert-management/tile.png)

按一下 hello**警示管理**磚 tooopen hello**警示管理**儀表板。  hello 儀表板會納入 hello 下表中的 hello 資料行。  每個資料行列出 hello 前 10 個警示計數比對資料行的準則 hello 指定領域和時間範圍。  您可以執行，即可提供 hello 整個清單的記錄搜尋**查看所有**底部 hello hello 資料行，或按一下 hello 資料行標頭。

| 資料欄 | 說明 |
|:--- |:--- |
| 重大警示 |嚴重性為「重大」的所有警示 (依警示名稱分組)。  按一下警示名稱 toorun 傳回該警示的所有記錄的記錄搜尋。 |
| 警告警示 |嚴重性為「警告」的所有警示 (依警示名稱分組)。  按一下警示名稱 toorun 傳回該警示的所有記錄的記錄搜尋。 |
| 作用中的 SCOM 警示 |所有警示都收集從 Operations Manager 與任何狀態以外*Closed*依來源分組該 hello 產生的警示。 |
| 所有作用中警示 |具有任何嚴重性的所有警示 (依警示名稱分組)。 只包含 [已關閉] 以外任何狀態的 Operations Manager 警示。 |

如果您將 toohello 向右捲動，hello 儀表板會列出數個常用的查詢，您可以按一下 tooperform[記錄搜尋](log-analytics-log-searches.md)警示資料。

![警示管理儀表板](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Log Analytics 記錄
hello 警示管理解決方案會分析具有類型的任何記錄**警示**。  記錄分析所建立，或從 Nagios 或 Zabbix 收集警示不會直接收集 hello 方案。

hello 方案未從 System Center Operations Manager 匯入警示，並針對每個類型為建立對應的記錄**警示**和的 SourceSystem **OpsManager**。  這些記錄 hello 下表中都有 hello 屬性：  

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |*警示* |
| SourceSystem |*OpsManager* |
| AlertContext |Hello 資料項目造成 hello 警示 toobe 產生 XML 格式的詳細資料。 |
| AlertDescription |Hello 警示的詳細的描述。 |
| AlertId |Hello 警示的 GUID。 |
| AlertName |Hello 警示名稱。 |
| AlertPriority |Hello 警示的優先順序層級。 |
| AlertSeverity |Hello 警示的嚴重性層級。 |
| AlertState |最新的 hello 警示的解決狀態。 |
| LastModifiedBy |上次修改 hello 警示的 hello 使用者的名稱。 |
| ManagementGroupName |Hello hello 警示產生的位置的管理群組的名稱。 |
| RepeatCount |次數相同的警示產生的 hello hello 相同自正在解析受監視物件。 |
| ResolvedBy |Hello，使用者已經解決的 hello 警示的名稱。 如果 hello 警示尚未解決的空白。 |
| SourceDisplayName |顯示 hello 監視產生 hello 警示的物件名稱。 |
| SourceFullName |Hello 監視產生 hello 警示的物件完整名稱。 |
| TicketId |如果與指派警示的票證的處理序整合 hello System Center Operations Manager 環境的 hello 警示的票證識別碼。  如果未指派票證識別碼，則為空白。 |
| TimeGenerated |建立的日期和 hello 警示的時間。 |
| TimeLastModified |上次變更日期和 hello 警示的時間。 |
| TimeRaised |已產生日期和 hello 警示的時間。 |
| TimeResolved |日期和時間 hello 警示已解決。 如果 hello 警示尚未解決的空白。 |

## <a name="sample-log-searches"></a>記錄檔搜尋範例
hello 下表提供此解決方案所收集的警示記錄的範例記錄檔搜尋： 

| 查詢 | 說明 |
|:--- |:--- |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR |在 hello 期間引發過去 24 小時內的重大警示 |
| Type=Alert AlertSeverity=warning TimeRaised>NOW-24HOUR |在 hello 期間引發過去 24 小時內的警告警示 |
| Type=Alert SourceSystem=OpsManager AlertState!=Closed TimeRaised>NOW-24HOUR &#124; measure count() as Count by SourceDisplayName |Hello 期間引發過去 24 小時內作用中警示的來源 |
| Type=Alert SourceSystem=OpsManager AlertSeverity=error TimeRaised>NOW-24HOUR AlertState!=Closed |引發 hello 期間仍在作用中的過去 24 小時內的重大警示 |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-24HOUR AlertState=Closed |產生期間 hello 現在已關閉的過去 24 小時內的警示 |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; measure count() as Count by AlertSeverity |Hello 依其嚴重性分組過去 1 天內引發的警示 |
| Type=Alert SourceSystem=OpsManager TimeRaised>NOW-1DAY &#124; sort RepeatCount desc |Hello 依其重複次數值排序過去 1 天內引發的警示 |


>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列：
>
>| 查詢 | 說明 |
|:---|:---|
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) |在 hello 期間引發過去 24 小時內的重大警示 |
| Alert &#124; where AlertSeverity == "warning" and TimeRaised > ago(24h) |在 hello 期間引發過去 24 小時內的警告警示 |
| Alert &#124; where SourceSystem == "OpsManager" and AlertState != "Closed" and TimeRaised > ago(24h) &#124; summarize Count = count() by SourceDisplayName |Hello 期間引發過去 24 小時內作用中警示的來源 |
| Alert &#124; where SourceSystem == "OpsManager" and AlertSeverity == "error" and TimeRaised > ago(24h) and AlertState != "Closed" |引發 hello 期間仍在作用中的過去 24 小時內的重大警示 |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(24h) and AlertState == "Closed" |產生期間 hello 現在已關閉的過去 24 小時內的警示 |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; summarize Count = count() by AlertSeverity |Hello 依其嚴重性分組過去 1 天內引發的警示 |
| Alert &#124; where SourceSystem == "OpsManager" and TimeRaised > ago(1d) &#124; sort by RepeatCount desc |Hello 依其重複次數值排序過去 1 天內引發的警示 |


## <a name="next-steps"></a>後續步驟
* 如需有關從 Log Analytics 產生的警示的詳細資料，請深入了解 [Log Analytics 中的警示](log-analytics-alerts.md) 。
