---
title: "在 OMS Log Analytics 中收集自訂 JSON 資料 | Microsoft Docs"
description: "您可以使用 OMS Agent for Linux 將自訂 JSON 資料來源收集到 Log Analytics 中。  這些自訂資料來源可以是會傳回 JSON 的簡單指令碼，例如 curl 或 FluentD 的 300 個以上的外掛程式之一。 本文說明此資料收集所需的設定。"
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
ms.openlocfilehash: 800ee1269556e7c2d56fbbf2b497c10509b5c78c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collecting-custom-json-data-sources-with-the-oms-agent-for-linux-in-log-analytics"></a><span data-ttu-id="80cc0-105">在 Log Analytics 中使用 OMS Agent for Linux 收集自訂 JSON 資料來源</span><span class="sxs-lookup"><span data-stu-id="80cc0-105">Collecting custom JSON data sources with the OMS Agent for Linux in Log Analytics</span></span>
<span data-ttu-id="80cc0-106">您可以使用 OMS Agent for Linux 將自訂 JSON 資料來源收集到 Log Analytics 中。</span><span class="sxs-lookup"><span data-stu-id="80cc0-106">Custom JSON data sources can be collected into Log Analytics using the OMS Agent for Linux.</span></span>  <span data-ttu-id="80cc0-107">這些自訂資料來源可以是會傳回 JSON 的簡單指令碼，例如 [curl](https://curl.haxx.se/) 或 [FluentD 的 300 個以上的外掛程式](http://www.fluentd.org/plugins/all)之一。</span><span class="sxs-lookup"><span data-stu-id="80cc0-107">These custom data sources can be simple scripts returning JSON such as [curl](https://curl.haxx.se/) or one of [FluentD's 300+ plugins](http://www.fluentd.org/plugins/all).</span></span> <span data-ttu-id="80cc0-108">本文說明此資料收集所需的設定。</span><span class="sxs-lookup"><span data-stu-id="80cc0-108">This article describes the configuration required for this data collection.</span></span>

> [!NOTE]
> <span data-ttu-id="80cc0-109">需要有 OMS Agent for Linux v1.1.0-217+ 才能收集自訂 JSON 資料</span><span class="sxs-lookup"><span data-stu-id="80cc0-109">OMS Agent for Linux v1.1.0-217+ is required for Custom JSON Data</span></span>

## <a name="configuration"></a><span data-ttu-id="80cc0-110">組態</span><span class="sxs-lookup"><span data-stu-id="80cc0-110">Configuration</span></span>

### <a name="configure-input-plugin"></a><span data-ttu-id="80cc0-111">設定輸入外掛程式</span><span class="sxs-lookup"><span data-stu-id="80cc0-111">Configure input plugin</span></span>

<span data-ttu-id="80cc0-112">若要在 Log Analytics 中收集 JSON 資料，請將 `oms.api.` 新增至輸入外掛程式中的 FluentD 標記開頭。</span><span class="sxs-lookup"><span data-stu-id="80cc0-112">To collect JSON data in Log Analytics, add `oms.api.` to the start of a FluentD tag in an input plugin.</span></span>

<span data-ttu-id="80cc0-113">例如，以下是 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` 中的個別設定檔 `exec-json.conf`。</span><span class="sxs-lookup"><span data-stu-id="80cc0-113">For example, following is a separate configuration file `exec-json.conf` in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`.</span></span>  <span data-ttu-id="80cc0-114">這會使用 FluentD 外掛程式 `exec` 每隔 30 秒執行一次 curl 命令。</span><span class="sxs-lookup"><span data-stu-id="80cc0-114">This uses the FluentD plugin `exec` to run a curl command every 30 seconds.</span></span>  <span data-ttu-id="80cc0-115">此命令的輸出由 JSON 輸出外掛程式所收集。</span><span class="sxs-lookup"><span data-stu-id="80cc0-115">The output from this command is collected by the JSON output plugin.</span></span>

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
<span data-ttu-id="80cc0-116">對於在 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` 下新增的設定檔，必須使用下列命令變更其擁有權。</span><span class="sxs-lookup"><span data-stu-id="80cc0-116">The configuration file added under `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` will require to have its ownership changed with the following command.</span></span>

`sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/conf/omsagent.d/exec-json.conf`

### <a name="configure-output-plugin"></a><span data-ttu-id="80cc0-117">設定輸出外掛程式</span><span class="sxs-lookup"><span data-stu-id="80cc0-117">Configure output plugin</span></span> 
<span data-ttu-id="80cc0-118">將下列輸出外掛程式設定新增至 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` 中的主要設定，或新增為個別的設定檔再放入 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/` 中</span><span class="sxs-lookup"><span data-stu-id="80cc0-118">Add the following output plugin configuration to the main configuration in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` or as a separate configuration file placed in `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/`</span></span>

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

### <a name="restart-oms-agent-for-linux"></a><span data-ttu-id="80cc0-119">重新啟動 OMS Agent for Linux</span><span class="sxs-lookup"><span data-stu-id="80cc0-119">Restart OMS Agent for Linux</span></span>
<span data-ttu-id="80cc0-120">使用下列命令重新啟動 OMS Agent for Linux 服務。</span><span class="sxs-lookup"><span data-stu-id="80cc0-120">Restart the OMS Agent for Linux service with the following command.</span></span>

    sudo /opt/microsoft/omsagent/bin/service_control restart 

## <a name="output"></a><span data-ttu-id="80cc0-121">輸出</span><span class="sxs-lookup"><span data-stu-id="80cc0-121">Output</span></span>
<span data-ttu-id="80cc0-122">Log Analytics 中將會收集資料，記錄類型為 `<FLUENTD_TAG>_CL`。</span><span class="sxs-lookup"><span data-stu-id="80cc0-122">The data will be collected in Log Analytics with a record type of `<FLUENTD_TAG>_CL`.</span></span>

<span data-ttu-id="80cc0-123">例如，Log Analytics 中的自訂標記 `tag oms.api.tomcat`，記錄類型為 `tomcat_CL`。</span><span class="sxs-lookup"><span data-stu-id="80cc0-123">For example, the custom tag `tag oms.api.tomcat` in Log Analytics with a record type of `tomcat_CL`.</span></span>  <span data-ttu-id="80cc0-124">您可以使用下列記錄搜尋來擷取此類型的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="80cc0-124">You could retrieve all records of this type with the following log search.</span></span>

    Type=tomcat_CL

<span data-ttu-id="80cc0-125">支援巢狀 JSON 資料來源，但編製索引是以父欄位作為基礎。</span><span class="sxs-lookup"><span data-stu-id="80cc0-125">Nested JSON data sources are supported, but are indexed based off of parent field.</span></span> <span data-ttu-id="80cc0-126">例如，Log Analytics 搜尋會以 `tag_s : "[{ "a":"1", "b":"2" }]` 傳回下列 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="80cc0-126">For example, the following JSON data is returned from a Log Analytics search as `tag_s : "[{ "a":"1", "b":"2" }]`.</span></span>

```
{
    "tag": [{
        "a":"1",
        "b":"2"
    }]
}
```


## <a name="next-steps"></a><span data-ttu-id="80cc0-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80cc0-127">Next steps</span></span>
* <span data-ttu-id="80cc0-128">了解 [記錄搜尋](log-analytics-log-searches.md) ，其可分析從資料來源和方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="80cc0-128">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
 