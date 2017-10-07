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
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="ebc21-104">在 Log Analytics 中，從 Linux 代理程式上的 CollectD 收集資料</span><span class="sxs-lookup"><span data-stu-id="ebc21-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="ebc21-105">[CollectD](https://collectd.org/) 是開放原始碼 Linux 精靈，可定期收集來自應用程式的效能計量和系統等級資訊。</span><span class="sxs-lookup"><span data-stu-id="ebc21-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="ebc21-106">範例應用程式包括 hello Java Virtual Machine (JVM)、 MySQL Server 和 Nginx。</span><span class="sxs-lookup"><span data-stu-id="ebc21-106">Example applications include hello Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="ebc21-107">本文提供如何在 Log Analytics 中從 CollectD 收集效能資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ebc21-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="ebc21-108">您可以在[外掛程式表](https://collectd.org/wiki/index.php/Table_of_Plugins)中找到可用之外掛程式的完整清單。</span><span class="sxs-lookup"><span data-stu-id="ebc21-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD 概觀](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="ebc21-110">hello 下列 CollectD 組態包含在 hello OMS Agent for Linux tooroute CollectD 資料 toohello OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="ebc21-110">hello following CollectD configuration is included in hello OMS Agent for Linux tooroute  CollectD data toohello OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="ebc21-111">此外，如果使用新版 collectD 5.5 使用 hello 改為下列組態之前。</span><span class="sxs-lookup"><span data-stu-id="ebc21-111">Additionally, if using an versions of collectD before 5.5 use hello following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="ebc21-112">hello CollectD 組態使用預設 hello`write_http`透過連接埠 26000 tooOMS Agent for Linux 的外掛程式 toosend 效能度量資料。</span><span class="sxs-lookup"><span data-stu-id="ebc21-112">hello CollectD configuration uses hello default`write_http` plugin toosend performance metric data over port 26000 tooOMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="ebc21-113">如有需要此連接埠可以是設定的 tooa 自訂連接埠。</span><span class="sxs-lookup"><span data-stu-id="ebc21-113">This port can be configured tooa custom-defined port if needed.</span></span>

<span data-ttu-id="ebc21-114">hello OMS Agent for Linux 也會接聽連接埠 26000 CollectD 度量，然後將它們轉換 tooOMS 結構描述的度量。</span><span class="sxs-lookup"><span data-stu-id="ebc21-114">hello OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them tooOMS schema metrics.</span></span> <span data-ttu-id="ebc21-115">hello 下列為 hello OMS Agent for Linux 組態`collectd.conf`。</span><span class="sxs-lookup"><span data-stu-id="ebc21-115">hello following is hello OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="ebc21-116">支援的版本</span><span class="sxs-lookup"><span data-stu-id="ebc21-116">Versions supported</span></span>
- <span data-ttu-id="ebc21-117">Log Analytics 目前支援 CollectD 4.8 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ebc21-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="ebc21-118">需要有 OMS Agent for Linux v1.1.0-217 或以上才能收集 CollectD 計量。</span><span class="sxs-lookup"><span data-stu-id="ebc21-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="ebc21-119">組態</span><span class="sxs-lookup"><span data-stu-id="ebc21-119">Configuration</span></span>
<span data-ttu-id="ebc21-120">hello 如下 CollectD 中的資料記錄分析的基本步驟 tooconfigure 集合。</span><span class="sxs-lookup"><span data-stu-id="ebc21-120">hello following are basic steps tooconfigure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="ebc21-121">設定 CollectD toosend 資料 toohello OMS Agent for Linux 使用 hello write_http 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="ebc21-121">Configure CollectD toosend data toohello OMS Agent for Linux using hello write_http plugin.</span></span>  
2. <span data-ttu-id="ebc21-122">Hello 適當連接埠上設定 hello OMS Agent for Linux toolisten hello CollectD 資料。</span><span class="sxs-lookup"><span data-stu-id="ebc21-122">Configure hello OMS Agent for Linux toolisten for hello CollectD data on hello appropriate port.</span></span>
3. <span data-ttu-id="ebc21-123">重新啟動 CollectD 和 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="ebc21-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-tooforward-data"></a><span data-ttu-id="ebc21-124">設定 CollectD tooforward 資料</span><span class="sxs-lookup"><span data-stu-id="ebc21-124">Configure CollectD tooforward data</span></span> 

1. <span data-ttu-id="ebc21-125">tooroute CollectD 資料 toohello OMS Agent for Linux，`oms.conf`需求 toobe 加入 tooCollectD 的設定目錄。</span><span class="sxs-lookup"><span data-stu-id="ebc21-125">tooroute CollectD data toohello OMS Agent for Linux, `oms.conf` needs toobe added tooCollectD's configuration directory.</span></span> <span data-ttu-id="ebc21-126">hello 這個檔案的目的地取決於您電腦的 hello Linux distro。</span><span class="sxs-lookup"><span data-stu-id="ebc21-126">hello destination of this file depends on hello Linux  distro of your machine.</span></span>

    <span data-ttu-id="ebc21-127">如果您的 CollectD 設定目錄位於 /etc/collectd.d/：</span><span class="sxs-lookup"><span data-stu-id="ebc21-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="ebc21-128">如果您的 CollectD 設定目錄位於 /etc/collectd/collectd.conf.d/：</span><span class="sxs-lookup"><span data-stu-id="ebc21-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="ebc21-129">CollectD 5.5 之前的版本中將有 toomodify hello 標記`oms.conf`如上所示。</span><span class="sxs-lookup"><span data-stu-id="ebc21-129">For CollectD versions before 5.5 you will have toomodify hello tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="ebc21-130">複製 collectd.conf toohello 所需的工作區的 omsagent 組態目錄。</span><span class="sxs-lookup"><span data-stu-id="ebc21-130">Copy collectd.conf toohello desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="ebc21-131">重新啟動 CollectD 與 OMS Agent for Linux 與 hello 下列命令。</span><span class="sxs-lookup"><span data-stu-id="ebc21-131">Restart CollectD and OMS Agent for Linux with hello following commands.</span></span>

    <span data-ttu-id="ebc21-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="ebc21-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-toolog-analytics-schema-conversion"></a><span data-ttu-id="ebc21-133">CollectD 度量 tooLog 分析結構描述轉換</span><span class="sxs-lookup"><span data-stu-id="ebc21-133">CollectD metrics tooLog Analytics schema conversion</span></span>
<span data-ttu-id="ebc21-134">toomaintain 熟悉的模型之間已用於 Linux 和 hello 新度量收集 OMS 的代理程式的基礎結構計量所收集的 CollectD 會使用下列結構描述對應的 hello:</span><span class="sxs-lookup"><span data-stu-id="ebc21-134">toomaintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and hello new metrics collected by CollectD hello following schema mapping is used:</span></span>

| <span data-ttu-id="ebc21-135">CollectD 計量欄位</span><span class="sxs-lookup"><span data-stu-id="ebc21-135">CollectD Metric field</span></span> | <span data-ttu-id="ebc21-136">Log Analytics 欄位</span><span class="sxs-lookup"><span data-stu-id="ebc21-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="ebc21-137">主機</span><span class="sxs-lookup"><span data-stu-id="ebc21-137">host</span></span> | <span data-ttu-id="ebc21-138">電腦</span><span class="sxs-lookup"><span data-stu-id="ebc21-138">Computer</span></span> |
| <span data-ttu-id="ebc21-139">plugin</span><span class="sxs-lookup"><span data-stu-id="ebc21-139">plugin</span></span> | <span data-ttu-id="ebc21-140">None</span><span class="sxs-lookup"><span data-stu-id="ebc21-140">None</span></span> |
| <span data-ttu-id="ebc21-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="ebc21-141">plugin_instance</span></span> | <span data-ttu-id="ebc21-142">執行個體名稱</span><span class="sxs-lookup"><span data-stu-id="ebc21-142">Instance Name</span></span><br><span data-ttu-id="ebc21-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="ebc21-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="ebc21-144">類型</span><span class="sxs-lookup"><span data-stu-id="ebc21-144">type</span></span> | <span data-ttu-id="ebc21-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="ebc21-145">ObjectName</span></span> |
| <span data-ttu-id="ebc21-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="ebc21-146">type_instance</span></span> | <span data-ttu-id="ebc21-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="ebc21-147">CounterName</span></span><br><span data-ttu-id="ebc21-148">If **type_instance** is *null* then CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="ebc21-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="ebc21-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="ebc21-149">dsnames[]</span></span> | <span data-ttu-id="ebc21-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="ebc21-150">CounterName</span></span> |
| <span data-ttu-id="ebc21-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="ebc21-151">dstypes</span></span> | <span data-ttu-id="ebc21-152">None</span><span class="sxs-lookup"><span data-stu-id="ebc21-152">None</span></span> |
| <span data-ttu-id="ebc21-153">values[]</span><span class="sxs-lookup"><span data-stu-id="ebc21-153">values[]</span></span> | <span data-ttu-id="ebc21-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="ebc21-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ebc21-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ebc21-155">Next steps</span></span>
* <span data-ttu-id="ebc21-156">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="ebc21-156">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="ebc21-157">使用[自訂欄位](log-analytics-custom-fields.md)tooparse syslog 記錄，到個別欄位的資料。</span><span class="sxs-lookup"><span data-stu-id="ebc21-157">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>

