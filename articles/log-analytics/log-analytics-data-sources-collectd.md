---
title: "在 OMS Log Analytics 中從 CollectD 收集資料 | Microsoft Docs"
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
ms.openlocfilehash: a63b15ca5126b45451f0694c9ee75d7b67b1ceaf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-data-from-collectd-on-linux-agents-in-log-analytics"></a><span data-ttu-id="13374-104">在 Log Analytics 中，從 Linux 代理程式上的 CollectD 收集資料</span><span class="sxs-lookup"><span data-stu-id="13374-104">Collect data from CollectD on Linux agents in Log Analytics</span></span>
<span data-ttu-id="13374-105">[CollectD](https://collectd.org/) 是開放原始碼 Linux 精靈，可定期收集來自應用程式的效能計量和系統等級資訊。</span><span class="sxs-lookup"><span data-stu-id="13374-105">[CollectD](https://collectd.org/) is an open source Linux daemon that periodically collects performance metrics from applications and system level information.</span></span> <span data-ttu-id="13374-106">範例應用程式包括 Java 虛擬機器 (JVM)、MySQL 伺服器和 Nginx。</span><span class="sxs-lookup"><span data-stu-id="13374-106">Example applications include the Java Virtual Machine (JVM), MySQL Server, and Nginx.</span></span> <span data-ttu-id="13374-107">本文提供如何在 Log Analytics 中從 CollectD 收集效能資料的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="13374-107">This article provides information on collecting performance data from CollectD in Log Analytics.</span></span>

<span data-ttu-id="13374-108">您可以在[外掛程式表](https://collectd.org/wiki/index.php/Table_of_Plugins)中找到可用之外掛程式的完整清單。</span><span class="sxs-lookup"><span data-stu-id="13374-108">A full list of available plugins can be found at [Table of Plugins](https://collectd.org/wiki/index.php/Table_of_Plugins).</span></span>

![CollectD 概觀](media/log-analytics-data-sources-collectd/overview.png)

<span data-ttu-id="13374-110">OMS Agent for Linux 包含下列 CollectD 設定，可將 CollectD 資料傳遞至 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="13374-110">The following CollectD configuration is included in the OMS Agent for Linux to route  CollectD data to the OMS Agent for Linux.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
         <Node "oms">
         URL "127.0.0.1:26000/oms.collectd"
         Format "JSON"
         StoreRates true
         </Node>
    </Plugin>

<span data-ttu-id="13374-111">此外，如果是使用 5.5 之前的 collectD 版本，請改為使用下列設定。</span><span class="sxs-lookup"><span data-stu-id="13374-111">Additionally, if using an versions of collectD before 5.5 use the following configuration instead.</span></span>

    LoadPlugin write_http

    <Plugin write_http>
       <URL "127.0.0.1:26000/oms.collectd">
        Format "JSON"
         StoreRates true
       </URL>
    </Plugin>

<span data-ttu-id="13374-112">CollectD 設定使用預設的 `write_http` 外掛程式，可將效能計量資料透過連接埠 26000 傳送至 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="13374-112">The CollectD configuration uses the default`write_http` plugin to send performance metric data over port 26000 to OMS Agent for Linux.</span></span> 

> [!NOTE]
> <span data-ttu-id="13374-113">如有需要，您可以將此連接埠設定為自行定義的連接埠。</span><span class="sxs-lookup"><span data-stu-id="13374-113">This port can be configured to a custom-defined port if needed.</span></span>

<span data-ttu-id="13374-114">OMS Agent for Linux 也會在連接埠 26000 接聽 CollectD 計量，然後將它們轉換成 OMS 結構描述計量。</span><span class="sxs-lookup"><span data-stu-id="13374-114">The OMS Agent for Linux also listens on port 26000 for CollectD metrics and then converts them to OMS schema metrics.</span></span> <span data-ttu-id="13374-115">以下是 OMS Agent for Linux 設定 `collectd.conf`。</span><span class="sxs-lookup"><span data-stu-id="13374-115">The following is the OMS Agent for Linux configuration  `collectd.conf`.</span></span>

    <source>
      type http
      port 26000
      bind 127.0.0.1
    </source>

    <filter oms.collectd>
      type filter_collectd
    </filter>


## <a name="versions-supported"></a><span data-ttu-id="13374-116">支援的版本</span><span class="sxs-lookup"><span data-stu-id="13374-116">Versions supported</span></span>
- <span data-ttu-id="13374-117">Log Analytics 目前支援 CollectD 4.8 版和更新版本。</span><span class="sxs-lookup"><span data-stu-id="13374-117">Log Analytics currently supports CollectD version 4.8 and above.</span></span>
- <span data-ttu-id="13374-118">需要有 OMS Agent for Linux v1.1.0-217 或以上才能收集 CollectD 計量。</span><span class="sxs-lookup"><span data-stu-id="13374-118">OMS Agent for Linux v1.1.0-217 or above is required for CollectD metric collection.</span></span>


## <a name="configuration"></a><span data-ttu-id="13374-119">組態</span><span class="sxs-lookup"><span data-stu-id="13374-119">Configuration</span></span>
<span data-ttu-id="13374-120">以下是在 Log Analytics 中設定收集 CollectD 資料的基本步驟。</span><span class="sxs-lookup"><span data-stu-id="13374-120">The following are basic steps to configure collection of CollectD data in Log Analytics.</span></span>

1. <span data-ttu-id="13374-121">使用 write_http 外掛程式，設定 CollectD 將資料傳送至 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="13374-121">Configure CollectD to send data to the OMS Agent for Linux using the write_http plugin.</span></span>  
2. <span data-ttu-id="13374-122">設定 OMS Agent for Linux 在適當的連接埠上接聽 CollectD 資料。</span><span class="sxs-lookup"><span data-stu-id="13374-122">Configure the OMS Agent for Linux to listen for the CollectD data on the appropriate port.</span></span>
3. <span data-ttu-id="13374-123">重新啟動 CollectD 和 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="13374-123">Restart CollectD and OMS Agent for Linux.</span></span>

### <a name="configure-collectd-to-forward-data"></a><span data-ttu-id="13374-124">設定 CollectD 來轉送資料</span><span class="sxs-lookup"><span data-stu-id="13374-124">Configure CollectD to forward data</span></span> 

1. <span data-ttu-id="13374-125">若要將 CollectD 資料傳遞至 OMS Agent for Linux，需要將 `oms.conf` 新增至 CollectD 的設定目錄。</span><span class="sxs-lookup"><span data-stu-id="13374-125">To route CollectD data to the OMS Agent for Linux, `oms.conf` needs to be added to CollectD's configuration directory.</span></span> <span data-ttu-id="13374-126">這個檔案的目的地取決於您電腦的 Linux 散發版本。</span><span class="sxs-lookup"><span data-stu-id="13374-126">The destination of this file depends on the Linux  distro of your machine.</span></span>

    <span data-ttu-id="13374-127">如果您的 CollectD 設定目錄位於 /etc/collectd.d/：</span><span class="sxs-lookup"><span data-stu-id="13374-127">If your CollectD config directory is located in /etc/collectd.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd.d/oms.conf

    <span data-ttu-id="13374-128">如果您的 CollectD 設定目錄位於 /etc/collectd/collectd.conf.d/：</span><span class="sxs-lookup"><span data-stu-id="13374-128">If your CollectD config directory is located in /etc/collectd/collectd.conf.d/:</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/oms.conf /etc/collectd/collectd.conf.d/oms.conf

    >[!NOTE]
    ><span data-ttu-id="13374-129">如果是 5.5 以前的 CollectD 版本，您就必須修改 `oms.conf` 中的標記，如上所示。</span><span class="sxs-lookup"><span data-stu-id="13374-129">For CollectD versions before 5.5 you will have to modify the tags in `oms.conf` as shown above.</span></span>
    >

2. <span data-ttu-id="13374-130">將 collectd.conf 複製到所需之工作區的 omsagent 設定目錄。</span><span class="sxs-lookup"><span data-stu-id="13374-130">Copy collectd.conf to the desired workspace's omsagent configuration directory.</span></span>

        sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.d/collectd.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/
        sudo chown omsagent:omiusers /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.d/collectd.conf

3. <span data-ttu-id="13374-131">使用下列命令重新啟動 CollectD 和 OMS Agent for Linux。</span><span class="sxs-lookup"><span data-stu-id="13374-131">Restart CollectD and OMS Agent for Linux with the following commands.</span></span>

    <span data-ttu-id="13374-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="13374-132">sudo service collectd restart  sudo /opt/microsoft/omsagent/bin/service_control restart</span></span>

## <a name="collectd-metrics-to-log-analytics-schema-conversion"></a><span data-ttu-id="13374-133">CollectD 計量至 Log Analytics 的結構描述轉換</span><span class="sxs-lookup"><span data-stu-id="13374-133">CollectD metrics to Log Analytics schema conversion</span></span>
<span data-ttu-id="13374-134">在 OMS Agent for Linux 已收集的基礎結構計量和 CollectD 所收集的新計量之間，為了維持一種熟悉的模型，我們使用下列結構描述對應：</span><span class="sxs-lookup"><span data-stu-id="13374-134">To maintain a familiar model between infrastructure metrics already collected by OMS Agent for Linux and the new metrics collected by CollectD the following schema mapping is used:</span></span>

| <span data-ttu-id="13374-135">CollectD 計量欄位</span><span class="sxs-lookup"><span data-stu-id="13374-135">CollectD Metric field</span></span> | <span data-ttu-id="13374-136">Log Analytics 欄位</span><span class="sxs-lookup"><span data-stu-id="13374-136">Log Analytics field</span></span> |
|:--|:--|
| <span data-ttu-id="13374-137">主機</span><span class="sxs-lookup"><span data-stu-id="13374-137">host</span></span> | <span data-ttu-id="13374-138">電腦</span><span class="sxs-lookup"><span data-stu-id="13374-138">Computer</span></span> |
| <span data-ttu-id="13374-139">plugin</span><span class="sxs-lookup"><span data-stu-id="13374-139">plugin</span></span> | <span data-ttu-id="13374-140">None</span><span class="sxs-lookup"><span data-stu-id="13374-140">None</span></span> |
| <span data-ttu-id="13374-141">plugin_instance</span><span class="sxs-lookup"><span data-stu-id="13374-141">plugin_instance</span></span> | <span data-ttu-id="13374-142">執行個體名稱</span><span class="sxs-lookup"><span data-stu-id="13374-142">Instance Name</span></span><br><span data-ttu-id="13374-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span><span class="sxs-lookup"><span data-stu-id="13374-143">If **plugin_instance** is *null* then InstanceName="*_Total*"</span></span> |
| <span data-ttu-id="13374-144">類型</span><span class="sxs-lookup"><span data-stu-id="13374-144">type</span></span> | <span data-ttu-id="13374-145">ObjectName</span><span class="sxs-lookup"><span data-stu-id="13374-145">ObjectName</span></span> |
| <span data-ttu-id="13374-146">type_instance</span><span class="sxs-lookup"><span data-stu-id="13374-146">type_instance</span></span> | <span data-ttu-id="13374-147">CounterName</span><span class="sxs-lookup"><span data-stu-id="13374-147">CounterName</span></span><br><span data-ttu-id="13374-148">If **type_instance** is *null* then CounterName=**blank**</span><span class="sxs-lookup"><span data-stu-id="13374-148">If **type_instance** is *null* then CounterName=**blank**</span></span> |
| <span data-ttu-id="13374-149">dsnames[]</span><span class="sxs-lookup"><span data-stu-id="13374-149">dsnames[]</span></span> | <span data-ttu-id="13374-150">CounterName</span><span class="sxs-lookup"><span data-stu-id="13374-150">CounterName</span></span> |
| <span data-ttu-id="13374-151">dstypes</span><span class="sxs-lookup"><span data-stu-id="13374-151">dstypes</span></span> | <span data-ttu-id="13374-152">None</span><span class="sxs-lookup"><span data-stu-id="13374-152">None</span></span> |
| <span data-ttu-id="13374-153">values[]</span><span class="sxs-lookup"><span data-stu-id="13374-153">values[]</span></span> | <span data-ttu-id="13374-154">CounterValue</span><span class="sxs-lookup"><span data-stu-id="13374-154">CounterValue</span></span> |

## <a name="next-steps"></a><span data-ttu-id="13374-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13374-155">Next steps</span></span>
* <span data-ttu-id="13374-156">了解 [記錄搜尋](log-analytics-log-searches.md) ，以分析從資料來源和解決方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="13374-156">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
* <span data-ttu-id="13374-157">使用 [自訂欄位](log-analytics-custom-fields.md) ，以將來自 syslog 記錄的資料剖析至個別欄位。</span><span class="sxs-lookup"><span data-stu-id="13374-157">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>

