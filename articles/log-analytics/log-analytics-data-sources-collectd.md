---
title: "在 OMS 記錄分析 CollectD aaaCollect 資料 |Microsoft 文件"
description: "CollectD 是開放原始碼 Linux 精靈，可定期收集來自應用程式的資料和系統等級資訊。  本文提供如何在 Log Analytics 中從 CollectD 收集資料的相關資訊。"
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
ms.date: 05/02/2017
ms.author: magoedte
ms.openlocfilehash: 7ad82c9c67a664aabd44f08bef2253d84cd2dfba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a>在 Log Analytics 中，從 Linux 代理程式上的 CollectD 收集資料
[CollectD](https://collectd.org/) 是開放原始碼 Linux 精靈，可定期收集來自應用程式的效能計量和系統等級資訊。 範例應用程式包括 hello Java Virtual Machine (JVM)、 MySQL Server 和 Nginx。 本文提供如何在 Log Analytics 中從 CollectD 收集效能資料的相關資訊。

您可以在[外掛程式表](https://collectd.org/wiki/index.php/Table_of_Plugins)中找到可用之外掛程式的完整清單。

![CollectD 概觀](media/log-analytics-data-sources-collectd/overview.png)

hello 下列 CollectD 組態包含在 hello OMS Agent for Linux tooroute CollectD 資料 toohello OMS Agent for Linux。

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

此外，如果使用新版 collectD 5.5 使用 hello 改為下列組態之前。

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

hello CollectD 組態使用預設 hello`write_http`透過連接埠 26000 tooOMS Agent for Linux 的外掛程式 toosend 效能度量資料。 

> [!NOTE]
> 如有需要此連接埠可以是設定的 tooa 自訂連接埠。

hello OMS Agent for Linux 也會接聽連接埠 26000 CollectD 度量，然後將它們轉換 tooOMS 結構描述的度量。 hello 下列為 hello OMS Agent for Linux 組態`collectd.conf`。

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a>支援的版本
- Log Analytics 目前支援 CollectD 4.8 版和更新版本。
- 需要有 OMS Agent for Linux v1.1.0-217 或以上才能收集 CollectD 計量。


## <a name="configuration"></a>組態
hello 如下 CollectD 中的資料記錄分析的基本步驟 tooconfigure 集合。

1. 設定 CollectD toosend 資料 toohello OMS Agent for Linux 使用 hello write_http 外掛程式。  
2. Hello 適當連接埠上設定 hello OMS Agent for Linux toolisten hello CollectD 資料。
3. 重新啟動 CollectD 和 OMS Agent for Linux。

### <a name="configure-collectd-tooforward-data"></a>設定 CollectD tooforward 資料 

1. tooroute CollectD 資料 toohello OMS Agent for Linux，`oms.conf`需求 toobe 加入 tooCollectD 的設定目錄。 hello 這個檔案的目的地取決於您電腦的 hello Linux distro。

    如果您的 CollectD 設定目錄位於 /etc/collectd.d/：

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    如果您的 CollectD 設定目錄位於 /etc/collectd/collectd.conf.d/：

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    >CollectD 5.5 之前的版本中將有 toomodify hello 標記`oms.conf`如上所示。
    >

2. 複製 collectd.conf toohello 所需的工作區的 omsagent 組態目錄。

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. 重新啟動 CollectD 與 OMS Agent for Linux 與 hello 下列命令。

    sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a>CollectD 度量 tooLog 分析結構描述轉換
toomaintain 熟悉的模型之間已用於 Linux 和 hello 新度量收集 OMS 的代理程式的基礎結構計量所收集的 CollectD 會使用下列結構描述對應的 hello:

| CollectD 計量欄位 | Log Analytics 欄位 |
|:--|:--|
| 主機 | 電腦 |
| plugin | None |
| plugin_instance | 執行個體名稱<br>If **plugin_instance** is *null* then InstanceName="*_Total*" |
| 類型 | ObjectName |
| type_instance | CounterName<br>If **type_instance** is *null* then CounterName=**blank** |
| dsnames[] | CounterName |
| dstypes | None |
| values[] | CounterValue |

## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。 
* 使用[自訂欄位](log-analytics-custom-fields.md)tooparse syslog 記錄，到個別欄位的資料。

