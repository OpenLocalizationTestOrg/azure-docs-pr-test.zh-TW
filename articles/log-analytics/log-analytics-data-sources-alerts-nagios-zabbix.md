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
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="6a552-105">從 OMS Agent for Linux 在 Log Analytics 中收集來自 Nagios 和 Zabbix 的警示</span><span class="sxs-lookup"><span data-stu-id="6a552-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="6a552-106">[Nagios](https://www.nagios.org/) 和 [Zabbix](http://www.zabbix.com/) 是開放原始碼監視工具。</span><span class="sxs-lookup"><span data-stu-id="6a552-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="6a552-107">您可以收集中的警示從這些工具到記錄分析順序 tooanalyze 它們連同[從其他來源的警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="6a552-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="6a552-108">本文說明 tooconfigure hello OMS Agent for Linux toocollect 從這些系統的發出警示。</span><span class="sxs-lookup"><span data-stu-id="6a552-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="6a552-109">設定警示收集</span><span class="sxs-lookup"><span data-stu-id="6a552-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="6a552-110">設定 Nagios 警示收集</span><span class="sxs-lookup"><span data-stu-id="6a552-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="6a552-111">執行下列步驟 hello Nagios 伺服器 toocollect 警示 hello。</span><span class="sxs-lookup"><span data-stu-id="6a552-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="6a552-112">授與 hello 使用者**omsagent**讀取權限 toohello Nagios 記錄檔 (也就是`/var/log/nagios/nagios.log`)。</span><span class="sxs-lookup"><span data-stu-id="6a552-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="6a552-113">假設 hello nagios.log 檔案由 hello 群組擁有`nagios`，您可以加入 hello 使用者**omsagent** toohello **nagios**群組。</span><span class="sxs-lookup"><span data-stu-id="6a552-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="6a552-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="6a552-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="6a552-115">修改在 hello 設定檔 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)。</span><span class="sxs-lookup"><span data-stu-id="6a552-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="6a552-116">請確定下列項目 hello 確實存在且未標成註解：</span><span class="sxs-lookup"><span data-stu-id="6a552-116">Ensure hello following entries are present and not commented out:</span></span>  

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

3. <span data-ttu-id="6a552-117">重新啟動 hello omsagent 精靈</span><span class="sxs-lookup"><span data-stu-id="6a552-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="6a552-118">設定 Zabbix 警示收集</span><span class="sxs-lookup"><span data-stu-id="6a552-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="6a552-119">toocollect Zabbix 伺服器的警示，您需要 toospecify 使用者和密碼*純文字*。</span><span class="sxs-lookup"><span data-stu-id="6a552-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="6a552-120">這不是理想的做法，但我們建議您建立 hello 使用者並授與權限 toomonitor onlu。</span><span class="sxs-lookup"><span data-stu-id="6a552-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="6a552-121">執行下列步驟 hello Nagios 伺服器 toocollect 警示 hello。</span><span class="sxs-lookup"><span data-stu-id="6a552-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="6a552-122">修改在 hello 設定檔 (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)。</span><span class="sxs-lookup"><span data-stu-id="6a552-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="6a552-123">請確定下列項目 hello 確實存在且未標成註解。變更 hello 使用者名稱和密碼 toovalues Zabbix 環境。</span><span class="sxs-lookup"><span data-stu-id="6a552-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="6a552-124">重新啟動 hello omsagent 精靈</span><span class="sxs-lookup"><span data-stu-id="6a552-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="6a552-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="6a552-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="6a552-126">警示記錄</span><span class="sxs-lookup"><span data-stu-id="6a552-126">Alert records</span></span>
<span data-ttu-id="6a552-127">您可以在 Log Analytics 中使用[記錄搜尋](log-analytics-log-searches.md)，擷取來自 Nagios 和 Zabbix 的警示記錄。</span><span class="sxs-lookup"><span data-stu-id="6a552-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="6a552-128">Nagios 警示記錄</span><span class="sxs-lookup"><span data-stu-id="6a552-128">Nagios Alert records</span></span>

<span data-ttu-id="6a552-129">Nagios 所收集之警示記錄的 **Type** 為 **Alert**，而 **SourceSystem** 為 **Nagios**。</span><span class="sxs-lookup"><span data-stu-id="6a552-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="6a552-130">所以在下表中的 hello 有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6a552-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="6a552-131">屬性</span><span class="sxs-lookup"><span data-stu-id="6a552-131">Property</span></span> | <span data-ttu-id="6a552-132">說明</span><span class="sxs-lookup"><span data-stu-id="6a552-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6a552-133">類型</span><span class="sxs-lookup"><span data-stu-id="6a552-133">Type</span></span> |<span data-ttu-id="6a552-134">*警示*</span><span class="sxs-lookup"><span data-stu-id="6a552-134">*Alert*</span></span> |
| <span data-ttu-id="6a552-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6a552-135">SourceSystem</span></span> |<span data-ttu-id="6a552-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="6a552-136">*Nagios*</span></span> |
| <span data-ttu-id="6a552-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="6a552-137">AlertName</span></span> |<span data-ttu-id="6a552-138">Hello 警示名稱。</span><span class="sxs-lookup"><span data-stu-id="6a552-138">Name of hello alert.</span></span> |
| <span data-ttu-id="6a552-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="6a552-139">AlertDescription</span></span> | <span data-ttu-id="6a552-140">Hello 警示的描述。</span><span class="sxs-lookup"><span data-stu-id="6a552-140">Description of hello alert.</span></span> |
| <span data-ttu-id="6a552-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="6a552-141">AlertState</span></span> | <span data-ttu-id="6a552-142">Hello 服務或主機的狀態。</span><span class="sxs-lookup"><span data-stu-id="6a552-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="6a552-143">OK</span><span class="sxs-lookup"><span data-stu-id="6a552-143">OK</span></span><br><span data-ttu-id="6a552-144">WARNING</span><span class="sxs-lookup"><span data-stu-id="6a552-144">WARNING</span></span><br><span data-ttu-id="6a552-145">UP</span><span class="sxs-lookup"><span data-stu-id="6a552-145">UP</span></span><br><span data-ttu-id="6a552-146">DOWN</span><span class="sxs-lookup"><span data-stu-id="6a552-146">DOWN</span></span> |
| <span data-ttu-id="6a552-147">HostName</span><span class="sxs-lookup"><span data-stu-id="6a552-147">HostName</span></span> | <span data-ttu-id="6a552-148">建立 hello 警示的 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6a552-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="6a552-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="6a552-149">PriorityNumber</span></span> | <span data-ttu-id="6a552-150">Hello 警示的優先順序層級。</span><span class="sxs-lookup"><span data-stu-id="6a552-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="6a552-151">StateType</span><span class="sxs-lookup"><span data-stu-id="6a552-151">StateType</span></span> | <span data-ttu-id="6a552-152">hello hello 警示狀態類型。</span><span class="sxs-lookup"><span data-stu-id="6a552-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="6a552-153">SOFT - 未重新檢查的問題。</span><span class="sxs-lookup"><span data-stu-id="6a552-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="6a552-154">HARD - 已依指定次數重新檢查的問題。</span><span class="sxs-lookup"><span data-stu-id="6a552-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="6a552-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="6a552-155">TimeGenerated</span></span> |<span data-ttu-id="6a552-156">建立日期和時間的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="6a552-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="6a552-157">Zabbix 警示記錄</span><span class="sxs-lookup"><span data-stu-id="6a552-157">Zabbix alert records</span></span>
<span data-ttu-id="6a552-158">Zabbix 所收集之警示記錄的 **Type** 為 **Alert**，而 **SourceSystem** 為 **Zabbix**。</span><span class="sxs-lookup"><span data-stu-id="6a552-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="6a552-159">所以在下表中的 hello 有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6a552-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="6a552-160">屬性</span><span class="sxs-lookup"><span data-stu-id="6a552-160">Property</span></span> | <span data-ttu-id="6a552-161">說明</span><span class="sxs-lookup"><span data-stu-id="6a552-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6a552-162">類型</span><span class="sxs-lookup"><span data-stu-id="6a552-162">Type</span></span> |<span data-ttu-id="6a552-163">*警示*</span><span class="sxs-lookup"><span data-stu-id="6a552-163">*Alert*</span></span> |
| <span data-ttu-id="6a552-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="6a552-164">SourceSystem</span></span> |<span data-ttu-id="6a552-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="6a552-165">*Zabbix*</span></span> |
| <span data-ttu-id="6a552-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="6a552-166">AlertName</span></span> | <span data-ttu-id="6a552-167">Hello 警示名稱。</span><span class="sxs-lookup"><span data-stu-id="6a552-167">Name of hello alert.</span></span> |
| <span data-ttu-id="6a552-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="6a552-168">AlertPriority</span></span> | <span data-ttu-id="6a552-169">Hello 警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="6a552-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="6a552-170">未分類</span><span class="sxs-lookup"><span data-stu-id="6a552-170">not classified</span></span><br><span data-ttu-id="6a552-171">資訊</span><span class="sxs-lookup"><span data-stu-id="6a552-171">information</span></span><br><span data-ttu-id="6a552-172">警告</span><span class="sxs-lookup"><span data-stu-id="6a552-172">warning</span></span><br><span data-ttu-id="6a552-173">average</span><span class="sxs-lookup"><span data-stu-id="6a552-173">average</span></span><br><span data-ttu-id="6a552-174">高</span><span class="sxs-lookup"><span data-stu-id="6a552-174">high</span></span><br><span data-ttu-id="6a552-175">嚴重損壞</span><span class="sxs-lookup"><span data-stu-id="6a552-175">disaster</span></span>  |
| <span data-ttu-id="6a552-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="6a552-176">AlertState</span></span> | <span data-ttu-id="6a552-177">Hello 警示的狀態。</span><span class="sxs-lookup"><span data-stu-id="6a552-177">State of hello alert.</span></span><br><br><span data-ttu-id="6a552-178">0-狀態已啟動 toodate。</span><span class="sxs-lookup"><span data-stu-id="6a552-178">0 - State is up toodate.</span></span><br><span data-ttu-id="6a552-179">1 - 狀態未知。</span><span class="sxs-lookup"><span data-stu-id="6a552-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="6a552-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="6a552-180">AlertTypeNumber</span></span> | <span data-ttu-id="6a552-181">指定警示是否可以產生多個問題事件。</span><span class="sxs-lookup"><span data-stu-id="6a552-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="6a552-182">0-狀態已啟動 toodate。</span><span class="sxs-lookup"><span data-stu-id="6a552-182">0 - State is up toodate.</span></span><br><span data-ttu-id="6a552-183">1 - 狀態未知。</span><span class="sxs-lookup"><span data-stu-id="6a552-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="6a552-184">註解</span><span class="sxs-lookup"><span data-stu-id="6a552-184">Comments</span></span> | <span data-ttu-id="6a552-185">警示的其他註解。</span><span class="sxs-lookup"><span data-stu-id="6a552-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="6a552-186">HostName</span><span class="sxs-lookup"><span data-stu-id="6a552-186">HostName</span></span> | <span data-ttu-id="6a552-187">建立 hello 警示的 hello 主機名稱。</span><span class="sxs-lookup"><span data-stu-id="6a552-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="6a552-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="6a552-188">PriorityNumber</span></span> | <span data-ttu-id="6a552-189">值，指出 hello 警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="6a552-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="6a552-190">0 - 未分類</span><span class="sxs-lookup"><span data-stu-id="6a552-190">0 - not classified</span></span><br><span data-ttu-id="6a552-191">1- 資訊</span><span class="sxs-lookup"><span data-stu-id="6a552-191">1 - information</span></span><br><span data-ttu-id="6a552-192">2 - 警告</span><span class="sxs-lookup"><span data-stu-id="6a552-192">2 - warning</span></span><br><span data-ttu-id="6a552-193">3 - 平均</span><span class="sxs-lookup"><span data-stu-id="6a552-193">3 - average</span></span><br><span data-ttu-id="6a552-194">4 - 高</span><span class="sxs-lookup"><span data-stu-id="6a552-194">4 - high</span></span><br><span data-ttu-id="6a552-195">5 - 嚴重損壞</span><span class="sxs-lookup"><span data-stu-id="6a552-195">5 - disaster</span></span> |
| <span data-ttu-id="6a552-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="6a552-196">TimeGenerated</span></span> |<span data-ttu-id="6a552-197">建立日期和時間的 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="6a552-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="6a552-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="6a552-198">TimeLastModified</span></span> |<span data-ttu-id="6a552-199">上次變更日期和時間的 hello 警示 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="6a552-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="6a552-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6a552-200">Next steps</span></span>
* <span data-ttu-id="6a552-201">了解 Log Analytics 中的[警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="6a552-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="6a552-202">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="6a552-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
