---
title: "aaaCollect 和分析 OMS 記錄分析中的 Windows 事件記錄檔 |Microsoft 文件"
description: "Windows 事件記錄檔是其中一種 hello 最常見的資料來源使用的記錄分析。  這篇文章描述如何 tooconfigure 收集 Windows 事件記錄檔和詳細資料的 hello 記錄它們建立 hello OMS 儲存機制中。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: ee52f564-995b-450f-a6ba-0d7b1dac3f32
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/15/2017
ms.author: bwren
ms.openlocfilehash: c05648af39258443f22fd11e1d751b5ccec8c391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a>Log Analytics 中的 Windows 事件記錄檔資料來源
Windows 事件記錄檔是其中一種最常見的 hello[資料來源](log-analytics-data-sources.md)針對使用 Windows 代理程式，因為許多應用程式寫入 toohello Windows 事件記錄檔收集資料。  您可以從收集事件中加入 toospecifying 在例如系統和應用程式的標準記錄檔建立的任何自訂記錄檔的應用程式中，您需要 toomonitor。

![Windows 事件](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a>設定 Windows 事件記錄檔
設定 Windows 事件記錄檔從 hello[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。

只記錄分析會從 hello hello 設定中指定的 Windows 事件記錄收集事件。  您可以將事件記錄檔加入 hello hello 記錄檔名稱中輸入，然後按一下 **+** 。  針對每個記錄檔，會收集的 hello 事件只有與選取的 hello 嚴重性。  請檢查您想 toocollect hello 特定記錄檔的 hello 嚴重性。  您無法提供任何其他準則 toofilter 事件。

當您輸入 hello 事件記錄檔名稱時，記錄分析會提供的一般事件記錄檔名稱的建議。 如果您想要 tooadd hello 記錄 hello 清單中沒有出現，您仍然可以將它輸入 hello hello 記錄檔的完整名稱。 您可以使用事件檢視器找到 hello hello 記錄檔的完整名稱。 在 事件檢視器中，開啟 hello*屬性*頁面 hello 記錄檔和複製 hello 字串 hello*全名*欄位。

![設定 Windows 事件](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a>資料收集
記錄分析會收集每個事件都必須符合所選的嚴重性從受監視的事件記錄檔所建立 hello 事件。  hello 代理程式會收集每個事件記錄檔中記錄其所在位置。  如果 hello 代理程式離線一段時間，然後記錄分析會收集事件從上次停止的地方，即使這些事件在 hello agent 離線期間所建立。  有可能會針對收集這些事件 toonot 若 hello 事件記錄檔會包裝與 hello 代理程式離線時遭到覆寫的回收事件。

>[!NOTE]
>Log Analytics 不會收集 SQL Server 從 *MSSQLSERVER* 來源用含有關鍵字 - *Classic* 或 *Audit Success* 的事件 ID 18453 以及用關鍵字 *0xa0000000000000* 所建立的稽核事件。
>

## <a name="windows-event-records-properties"></a>Windows 事件記錄屬性
Windows 事件記錄都有一種**事件**和 hello 下表中都有 hello 屬性：

| 屬性 | 說明 |
|:--- |:--- |
| 電腦 |從收集 hello hello 事件的電腦名稱。 |
| EventCategory |Hello 事件類別目錄。 |
| EventData |原始格式的所有事件資料。 |
| EventID |Hello 事件數目。 |
| EventLevel |數值格式中的 hello 事件的嚴重性。 |
| EventLevelName |以文字格式的 hello 事件的嚴重性。 |
| EventLog |從收集 hello 事件 hello 事件記錄檔名稱。 |
| ParameterXml |XML 格式的事件參數值。 |
| ManagementGroupName |System Center Operations Manager 代理程式 hello 管理群組名稱。  若為其他代理程式，此值為 AOI-<workspace ID>。 |
| RenderedDescription |含參數值的事件描述 |
| 來源 |Hello 事件的來源。 |
| SourceSystem |從已收集的代理程式 hello 事件類型。 <br> OpsManager - Windows 代理程式，直接連接或由 Operations Manager 管理 <br> Linux – 所有的 Linux 代理程式  <br> AzureStorage – Azure 診斷 |
| TimeGenerated |在 Windows 中，已建立日期和時間的 hello 事件。 |
| UserName |記錄 hello 事件 hello 帳戶使用者名稱。 |

## <a name="log-searches-with-windows-events"></a>使用 Windows 事件的記錄搜尋
hello 下表提供不同範例擷取 Windows 事件記錄的記錄搜尋。

| 查詢 | 說明 |
|:--- |:--- |
| Type=Event |所有的 Windows 事件。 |
| Type=Event EventLevelName=error |所有 Windows 事件與錯誤的嚴重性。 |
| Type=Event &#124; Measure count() by Source |依據來源的 Windows 事件計數。 |
| Type=Event EventLevelName=error &#124; Measure count() by Source |依據來源的 Windows 錯誤事件計數。 |


>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。
>
>| 查詢 | 說明 |
|:---|:---|
| Event |所有的 Windows 事件。 |
| Event &#124; where EventLevelName == "error" |所有 Windows 事件與錯誤的嚴重性。 |
| Event &#124; summarize count() by Source |依據來源的 Windows 事件計數。 |
| Event &#124; where EventLevelName == "error" &#124; summarize count() by Source |依據來源的 Windows 錯誤事件計數。 |


## <a name="next-steps"></a>後續步驟
* 設定記錄分析 toocollect 其他[資料來源](log-analytics-data-sources.md)進行分析。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。  
* 使用[自訂欄位](log-analytics-custom-fields.md)tooparse hello 事件記錄，到個別的欄位。
* 設定從您的 Windows 代理程式進行 [效能計數器收集](log-analytics-data-sources-performance-counters.md) 。
