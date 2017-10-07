---
title: "在 OMS 記錄分析的 aaaCollect Nagios 和 Zabbix 警示 |Microsoft 文件"
description: "Nagios 和 Zabbix 是開放原始碼監視工具。 您可以收集警示從這些工具到記錄分析中順序 tooanalyze 它們以及從其他來源的警示。  本文說明 tooconfigure hello OMS Agent for Linux toocollect 從這些系統的發出警示。"
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a>從 OMS Agent for Linux 在 Log Analytics 中收集來自 Nagios 和 Zabbix 的警示 
[Nagios](https://www.nagios.org/) 和 [Zabbix](http://www.zabbix.com/) 是開放原始碼監視工具。  您可以收集中的警示從這些工具到記錄分析順序 tooanalyze 它們連同[從其他來源的警示](log-analytics-alerts.md)。  本文說明 tooconfigure hello OMS Agent for Linux toocollect 從這些系統的發出警示。
 
## <a name="configure-alert-collection"></a>設定警示收集

### <a name="configuring-nagios-alert-collection"></a>設定 Nagios 警示收集
執行下列步驟 hello Nagios 伺服器 toocollect 警示 hello。

1. 授與 hello 使用者**omsagent**讀取權限 toohello Nagios 記錄檔 (也就是`/var/log/nagios/nagios.log`)。 假設 hello nagios.log 檔案由 hello 群組擁有`nagios`，您可以加入 hello 使用者**omsagent** toohello **nagios**群組。 

    sudo usermod -a -G nagios omsagent

2.  修改在 hello 設定檔 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)。 請確定下列項目 hello 確實存在且未標成註解：  

        <source>  
          type tail  
          #Update path toopoint tooyour nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. 重新啟動 hello omsagent 精靈

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a>設定 Zabbix 警示收集
toocollect Zabbix 伺服器的警示，您需要 toospecify 使用者和密碼*純文字*。 這不是理想的做法，但我們建議您建立 hello 使用者並授與權限 toomonitor onlu。

執行下列步驟 hello Nagios 伺服器 toocollect 警示 hello。

1. 修改在 hello 設定檔 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)。 請確定下列項目 hello 確實存在且未標成註解。變更 hello 使用者名稱和密碼 toovalues Zabbix 環境。

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. 重新啟動 hello omsagent 精靈

    sudo sh /opt/microsoft/omsagent/bin/service_control restart


## <a name="alert-records"></a>警示記錄
您可以在 Log Analytics 中使用[記錄搜尋](log-analytics-log-searches.md)，擷取來自 Nagios 和 Zabbix 的警示記錄。

### <a name="nagios-alert-records"></a>Nagios 警示記錄

Nagios 所收集之警示記錄的 **Type** 為 **Alert**，而 **SourceSystem** 為 **Nagios**。  所以在下表中的 hello 有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |*警示* |
| SourceSystem |*Nagios* |
| AlertName |Hello 警示名稱。 |
| AlertDescription | Hello 警示的描述。 |
| AlertState | Hello 服務或主機的狀態。<br><br>OK<br>WARNING<br>UP<br>DOWN |
| HostName | 建立 hello 警示的 hello 主機名稱。 |
| PriorityNumber | Hello 警示的優先順序層級。 |
| StateType | hello hello 警示狀態類型。<br><br>SOFT - 未重新檢查的問題。<br>HARD - 已依指定次數重新檢查的問題。  |
| TimeGenerated |建立日期和時間的 hello 警示。 |


### <a name="zabbix-alert-records"></a>Zabbix 警示記錄
Zabbix 所收集之警示記錄的 **Type** 為 **Alert**，而 **SourceSystem** 為 **Zabbix**。  所以在下表中的 hello 有 hello 屬性。

| 屬性 | 說明 |
|:--- |:--- |
| 類型 |*警示* |
| SourceSystem |*Zabbix* |
| AlertName | Hello 警示名稱。 |
| AlertPriority | Hello 警示的嚴重性。<br><br>未分類<br>資訊<br>警告<br>average<br>高<br>嚴重損壞  |
| AlertState | Hello 警示的狀態。<br><br>0-狀態已啟動 toodate。<br>1 - 狀態未知。  |
| AlertTypeNumber | 指定警示是否可以產生多個問題事件。<br><br>0-狀態已啟動 toodate。<br>1 - 狀態未知。    |
| 註解 | 警示的其他註解。 |
| HostName | 建立 hello 警示的 hello 主機名稱。 |
| PriorityNumber | 值，指出 hello 警示的嚴重性。<br><br>0 - 未分類<br>1- 資訊<br>2 - 警告<br>3 - 平均<br>4 - 高<br>5 - 嚴重損壞 |
| TimeGenerated |建立日期和時間的 hello 警示。 |
| TimeLastModified |上次變更日期和時間的 hello 警示 hello 狀態。 |


## <a name="next-steps"></a>後續步驟
* 了解 Log Analytics 中的[警示](log-analytics-alerts.md)。
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。 
