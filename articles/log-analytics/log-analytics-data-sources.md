---
title: "aaaConfigure OMS 記錄分析的資料來源 |Microsoft 文件"
description: "資料來源定義 hello 資料從代理程式和其他的記錄分析會收集連接的來源。  這篇文章描述如何記錄分析會使用資料來源的 hello 概念，說明 hello 詳細資料請參閱 tooconfigure 它們，並提供可用的 hello 不同資料來源的摘要。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 67710115-c861-40f8-a377-57c7fa6909b4
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: ebe8d29a2442a654b98004f624181ff406868e2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-in-log-analytics"></a>Log Analytics 中的資料來源
記錄分析會從您的 OMS 工作區中的 hello 連線來源收集資料，並將它儲存在 OMS 儲存機制。  從每個收集的 hello 資料是由 hello 您設定的資料來源定義。  Hello OMS 儲存機制中的資料會儲存為一組記錄。  每個資料來源都會建立特定類型的記錄，每種類型各有自己的一組屬性。

![Log Analytics 資料收集](./media/log-analytics-data-sources/overview.png)

資料來源是不同 OMS 解決方案也從連接的來源收集資料，並在 hello OMS 儲存機制中建立記錄。  方案可加入 tooyour 工作區中的 hello 解決方案資源庫，和通常會提供額外的分析工具 hello OMS 入口網站中。  

## <a name="summary-of-data-sources"></a>資料來源的摘要
目前可用於記錄分析的 hello 資料來源會列在下表中的 hello。  每個有連結 tooa 其他文章另提供該資料來源的詳細資料。

| 資料來源 | 事件類型 | 說明 |
|:--- |:--- |:--- |
| [自訂的記錄檔](log-analytics-data-sources-custom-logs.md) |\<LogName\>_CL |Windows 或 Linux 代理程式上包含記錄資訊的文字檔。 |
| [Windows 事件記錄檔](log-analytics-data-sources-windows-events.md) |Event |Windows 電腦上，從 hello 事件記錄檔收集事件。 |
| [Windows 效能計數器](log-analytics-data-sources-performance-counters.md) |Perf |從 Windows 電腦收集的效能計數器。 |
| [Linux 效能計數器](log-analytics-data-sources-performance-counters.md) |Perf |從 Linux 電腦收集的效能計數器。 |
| [IIS 記錄檔](log-analytics-data-sources-iis-logs.md) |W3CIISLog |W3C 格式的網際網路資訊服務記錄檔。 |
| [Syslog](log-analytics-data-sources-syslog.md) |syslog |Windows 或 Linux 電腦上的 Syslog 事件。 |

## <a name="configuring-data-sources"></a>設定資料來源
設定資料來源從 hello**資料**記錄分析中的功能表**設定**。  任何組態會傳遞 tooall 連接您的 OMS 工作區中的來源。  您目前無法透過這項組態來排除任何代理程式。

![設定 Windows 事件](./media/log-analytics-data-sources/configure-events.png)

1. 在 hello OMS 主控台中，按一下 hello**設定**磚或 hello**設定**在 hello 囉 」 畫面最上方的按鈕。
2. 選取 [資料] 。
3. 按一下 hello 資料來源 tooconfigure。
4. 按照其組態中每個資料來源以取得詳細資料資料表上方的 hello hello 連結 toohello 文件。

> [!NOTE]
> 您目前無法在 hello Azure 入口網站中設定記錄分析資料來源。

## <a name="data-collection"></a>資料收集
資料來源組態會傳遞 tooagents 內，則會直接連接的 tooLog 分析幾分鐘的時間。  hello 指定從 hello 代理程式收集資料並將其直接傳遞 tooLog 分析在特定 tooeach 間隔的資料來源。  請參閱每個資料來源，針對這些特性的 hello 文件。

已連線的管理群組中的 System Center Operations Manager (SCOM) 代理程式，資料來源組態會轉譯為管理組件，並傳遞 toohello 管理群組的設定，每隔 5 分鐘預設。  hello 代理程式下載 hello 如同任何其他的管理組件，並收集 hello 指定的資料。 根據 hello 資料來源 hello 資料將會是傳送 hello 資料 toohello 記錄分析會將轉送 tooa 管理伺服器或 hello 代理程式會傳送 hello 資料 tooLog 分析，而不需要透過 hello 管理伺服器。 請參閱太[OMS 功能和解決方案的詳細資料集合](log-analytics-add-solutions.md#data-collection-details)如需詳細資訊。  您可以閱讀 SCOM 和 OMS 的連線和修改 hello 頻率的詳細資料，設定在傳遞[Configure Integration with System Center Operations Manager](log-analytics-om-agents.md)。

如果分析或 Operations Manager 無法 tooconnect tooLog hello 代理程式，它會繼續它建立連接時，它會將傳遞的 toocollect 資料。  如果 hello 資料量達到 hello 快取大小上限為 hello 用戶端，或如果 hello 代理程式不能 tooestablish 24 小時內的連接，可能會遺失資料。

## <a name="log-analytics-records"></a>Log Analytics 記錄
為記錄，記錄分析所收集的所有資料都會都儲存在 hello OMS 儲存機制。  不同資料來源所收集的記錄會有自己的一組屬性，並由其 **類型** 屬性來識別。  每個記錄的型別，請參閱每個資料來源的 hello 文件集和解決方案的詳細資料。

## <a name="next-steps"></a>後續步驟
* 深入了解[解決方案](log-analytics-add-solutions.md)的新增功能 tooLog 分析和也可將資料收集到 hello OMS 儲存機制。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。  
* 設定[警示](log-analytics-alerts.md)tooproactively 通知您收集的資料來源和解決方案的重要資料。
