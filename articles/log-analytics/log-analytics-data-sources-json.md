---
title: "在 OMS 記錄分析 aaaCollecting 自訂 JSON 資料 |Microsoft 文件"
description: "JSON 資料的自訂來源可以收集到記錄分析使用 hello OMS Agent for Linux。  這些自訂資料來源可以是會傳回 JSON 的簡單指令碼，例如 curl 或 FluentD 的 300 個以上的外掛程式之一。 本文將針對此資料收集所需的 hello 設定。"
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
ms.openlocfilehash: 97d401408a8c206d4a9ef2ec9b13ba1ca6b5e92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="collecting-custom-json-data-sources-with-hello-oms-agent-for-linux-in-log-analytics"></a>以 hello OMS Agent for Linux 的記錄分析收集自訂 JSON 資料來源
JSON 資料的自訂來源可以收集到記錄分析使用 hello OMS Agent for Linux。  這些自訂資料來源可以是會傳回 JSON 的簡單指令碼，例如 [curl](https://curl.haxx.se/) 或 [FluentD 的 300 個以上的外掛程式](http://www.fluentd.org/plugins/all)之一。 本文將針對此資料收集所需的 hello 設定。

> [!NOTE]
> 需要有 OMS Agent for Linux v1.1.0-217+ 才能收集自訂 JSON 資料

## <a name="configuration"></a>組態

### <a name="configure-input-plugin"></a>設定輸入外掛程式

toocollect JSON 資料，記錄分析中的加入`oms.api.`toohello 開頭 FluentD 標籤中輸入的外掛程式。

例如，以下是 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` 中的個別設定檔 `exec-json.conf`。  這會使用 hello FluentD 外掛程式`exec`toorun curl 命令每隔 30 秒。  hello 輸出此命令會收集 hello JSON 輸出的外掛程式。

```
<source>
  type exec
  command 'curl localhost/json.output'
  format json
  tag oms.api.httpresponse
  run_interval 30s
</source>

<match oms.api.httpresponse>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api_httpresponse*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```
hello 設定檔新增至 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`需要的 toohave 的擁有權變更以 hello 下列命令。

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a>設定輸出外掛程式 
新增下列輸出外掛程式設定 toohello 主要組態中的 hello`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`或不同的組態檔放入`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`

```
<match oms.api.**>
  type out_oms_api
  log_level info

  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms_api*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
```

### <a name="restart-oms-agent-for-linux"></a>重新啟動 OMS Agent for Linux
重新啟動 hello OMS Agent for Linux 服務以 hello 下列命令。

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a>輸出
hello 資料將會收集記錄分析記錄類型為`<FLUENTD_TAG>_CL`。

例如，hello 自訂標籤`tag oms.api.tomcat`中記錄分析記錄類型為`tomcat_CL`。  您可以以下列記錄搜尋 hello 擷取這個類型的所有記錄。

    Type=tomcat_CL

支援巢狀 JSON 資料來源，但編製索引是以父欄位作為基礎。 例如，下列 JSON 資料的 hello 會傳回從做為記錄分析搜尋`tag_s : "[{ "a":"1", "b":"2" }]`。

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a>後續步驟
* 深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。 
 