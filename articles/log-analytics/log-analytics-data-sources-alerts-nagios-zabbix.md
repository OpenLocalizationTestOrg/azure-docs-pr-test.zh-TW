---
title: "在 OMS Log Analytics 中收集 Nagios 和 Zabbix 警示 | Microsoft Docs"
description: "Nagios 和 Zabbix 是開放原始碼監視工具。 您可以將來自這些工具的警示收集到 Log Analytics，以搭配其他來源的警示一起分析。  本文說明如何設定 OMS Agent for Linux 以收集來自這些系統的警示。"
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="18689-105">從 OMS Agent for Linux 在 Log Analytics 中收集來自 Nagios 和 Zabbix 的警示</span><span class="sxs-lookup"><span data-stu-id="18689-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="18689-106">[Nagios](https://www.nagios.org/) 和 [Zabbix](http://www.zabbix.com/) 是開放原始碼監視工具。</span><span class="sxs-lookup"><span data-stu-id="18689-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="18689-107">您可以將來自這些工具的警示收集到 Log Analytics，以搭配[其他來源的警示](log-analytics-alerts.md)一起分析。</span><span class="sxs-lookup"><span data-stu-id="18689-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="18689-108">本文說明如何設定 OMS Agent for Linux 以收集來自這些系統的警示。</span><span class="sxs-lookup"><span data-stu-id="18689-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="18689-109">設定警示收集</span><span class="sxs-lookup"><span data-stu-id="18689-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="18689-110">設定 Nagios 警示收集</span><span class="sxs-lookup"><span data-stu-id="18689-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="18689-111">在 Nagios 伺服器上執行下列步驟來收集警示。</span><span class="sxs-lookup"><span data-stu-id="18689-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="18689-112">將 Nagios 記錄檔 (即 `/var/log/nagios/nagios.log`) 的讀取權授與使用者 **omsagent**。</span><span class="sxs-lookup"><span data-stu-id="18689-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="18689-113">假設 nagios.log 檔案是由 `nagios` 群組所擁有，您可以將使用者 **omsagent** 新增至 **nagios** 群組。</span><span class="sxs-lookup"><span data-stu-id="18689-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="18689-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="18689-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="18689-115">編輯組態檔 (位於 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)。</span><span class="sxs-lookup"><span data-stu-id="18689-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="18689-116">確定下列項目存在且未標成註解︰</span><span class="sxs-lookup"><span data-stu-id="18689-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="18689-117">重新啟動 omsagent 精靈</span><span class="sxs-lookup"><span data-stu-id="18689-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="18689-118">設定 Zabbix 警示收集</span><span class="sxs-lookup"><span data-stu-id="18689-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="18689-119">若要收集來自 Zabbix 伺服器的警示，您需要以「純文字」指定使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="18689-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="18689-120">這雖然不理想，但建議您建立使用者，而且只授與監視權限。</span><span class="sxs-lookup"><span data-stu-id="18689-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="18689-121">在 Nagios 伺服器上執行下列步驟來收集警示。</span><span class="sxs-lookup"><span data-stu-id="18689-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="18689-122">編輯組態檔 (位於 `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`)。</span><span class="sxs-lookup"><span data-stu-id="18689-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="18689-123">確定下列項目存在且未標成註解。</span><span class="sxs-lookup"><span data-stu-id="18689-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="18689-124">將使用者名稱和密碼變更為您的 Zabbix 環境值。</span><span class="sxs-lookup"><span data-stu-id="18689-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="18689-125">重新啟動 omsagent 精靈</span><span class="sxs-lookup"><span data-stu-id="18689-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="18689-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="18689-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="18689-127">警示記錄</span><span class="sxs-lookup"><span data-stu-id="18689-127">Alert records</span></span>
<span data-ttu-id="18689-128">您可以在 Log Analytics 中使用[記錄搜尋](log-analytics-log-searches.md)，擷取來自 Nagios 和 Zabbix 的警示記錄。</span><span class="sxs-lookup"><span data-stu-id="18689-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="18689-129">Nagios 警示記錄</span><span class="sxs-lookup"><span data-stu-id="18689-129">Nagios Alert records</span></span>

<span data-ttu-id="18689-130">Nagios 所收集之警示記錄的 **Type** 為 **Alert**，而 **SourceSystem** 為 **Nagios**。</span><span class="sxs-lookup"><span data-stu-id="18689-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="18689-131">其屬性如下表所示。</span><span class="sxs-lookup"><span data-stu-id="18689-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="18689-132">屬性</span><span class="sxs-lookup"><span data-stu-id="18689-132">Property</span></span> | <span data-ttu-id="18689-133">說明</span><span class="sxs-lookup"><span data-stu-id="18689-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18689-134">類型</span><span class="sxs-lookup"><span data-stu-id="18689-134">Type</span></span> |<span data-ttu-id="18689-135">*警示*</span><span class="sxs-lookup"><span data-stu-id="18689-135">*Alert*</span></span> |
| <span data-ttu-id="18689-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="18689-136">SourceSystem</span></span> |<span data-ttu-id="18689-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="18689-137">*Nagios*</span></span> |
| <span data-ttu-id="18689-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="18689-138">AlertName</span></span> |<span data-ttu-id="18689-139">警示的名稱。</span><span class="sxs-lookup"><span data-stu-id="18689-139">Name of the alert.</span></span> |
| <span data-ttu-id="18689-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="18689-140">AlertDescription</span></span> | <span data-ttu-id="18689-141">警示的描述。</span><span class="sxs-lookup"><span data-stu-id="18689-141">Description of the alert.</span></span> |
| <span data-ttu-id="18689-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="18689-142">AlertState</span></span> | <span data-ttu-id="18689-143">服務或主機的狀態。</span><span class="sxs-lookup"><span data-stu-id="18689-143">Status of the service or host.</span></span><br><br><span data-ttu-id="18689-144">OK</span><span class="sxs-lookup"><span data-stu-id="18689-144">OK</span></span><br><span data-ttu-id="18689-145">WARNING</span><span class="sxs-lookup"><span data-stu-id="18689-145">WARNING</span></span><br><span data-ttu-id="18689-146">UP</span><span class="sxs-lookup"><span data-stu-id="18689-146">UP</span></span><br><span data-ttu-id="18689-147">DOWN</span><span class="sxs-lookup"><span data-stu-id="18689-147">DOWN</span></span> |
| <span data-ttu-id="18689-148">HostName</span><span class="sxs-lookup"><span data-stu-id="18689-148">HostName</span></span> | <span data-ttu-id="18689-149">建立警示的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="18689-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="18689-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="18689-150">PriorityNumber</span></span> | <span data-ttu-id="18689-151">警示的優先順序層級。</span><span class="sxs-lookup"><span data-stu-id="18689-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="18689-152">StateType</span><span class="sxs-lookup"><span data-stu-id="18689-152">StateType</span></span> | <span data-ttu-id="18689-153">警示的狀態類型。</span><span class="sxs-lookup"><span data-stu-id="18689-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="18689-154">SOFT - 未重新檢查的問題。</span><span class="sxs-lookup"><span data-stu-id="18689-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="18689-155">HARD - 已依指定次數重新檢查的問題。</span><span class="sxs-lookup"><span data-stu-id="18689-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="18689-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="18689-156">TimeGenerated</span></span> |<span data-ttu-id="18689-157">建立警示的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="18689-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="18689-158">Zabbix 警示記錄</span><span class="sxs-lookup"><span data-stu-id="18689-158">Zabbix alert records</span></span>
<span data-ttu-id="18689-159">Zabbix 所收集之警示記錄的 **Type** 為 **Alert**，而 **SourceSystem** 為 **Zabbix**。</span><span class="sxs-lookup"><span data-stu-id="18689-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="18689-160">其屬性如下表所示。</span><span class="sxs-lookup"><span data-stu-id="18689-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="18689-161">屬性</span><span class="sxs-lookup"><span data-stu-id="18689-161">Property</span></span> | <span data-ttu-id="18689-162">說明</span><span class="sxs-lookup"><span data-stu-id="18689-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="18689-163">類型</span><span class="sxs-lookup"><span data-stu-id="18689-163">Type</span></span> |<span data-ttu-id="18689-164">*警示*</span><span class="sxs-lookup"><span data-stu-id="18689-164">*Alert*</span></span> |
| <span data-ttu-id="18689-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="18689-165">SourceSystem</span></span> |<span data-ttu-id="18689-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="18689-166">*Zabbix*</span></span> |
| <span data-ttu-id="18689-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="18689-167">AlertName</span></span> | <span data-ttu-id="18689-168">警示的名稱。</span><span class="sxs-lookup"><span data-stu-id="18689-168">Name of the alert.</span></span> |
| <span data-ttu-id="18689-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="18689-169">AlertPriority</span></span> | <span data-ttu-id="18689-170">警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="18689-170">Severity of the alert.</span></span><br><br><span data-ttu-id="18689-171">未分類</span><span class="sxs-lookup"><span data-stu-id="18689-171">not classified</span></span><br><span data-ttu-id="18689-172">資訊</span><span class="sxs-lookup"><span data-stu-id="18689-172">information</span></span><br><span data-ttu-id="18689-173">警告</span><span class="sxs-lookup"><span data-stu-id="18689-173">warning</span></span><br><span data-ttu-id="18689-174">average</span><span class="sxs-lookup"><span data-stu-id="18689-174">average</span></span><br><span data-ttu-id="18689-175">高</span><span class="sxs-lookup"><span data-stu-id="18689-175">high</span></span><br><span data-ttu-id="18689-176">嚴重損壞</span><span class="sxs-lookup"><span data-stu-id="18689-176">disaster</span></span>  |
| <span data-ttu-id="18689-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="18689-177">AlertState</span></span> | <span data-ttu-id="18689-178">警示的狀態。</span><span class="sxs-lookup"><span data-stu-id="18689-178">State of the alert.</span></span><br><br><span data-ttu-id="18689-179">0 - 最新狀態。</span><span class="sxs-lookup"><span data-stu-id="18689-179">0 - State is up to date.</span></span><br><span data-ttu-id="18689-180">1 - 狀態未知。</span><span class="sxs-lookup"><span data-stu-id="18689-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="18689-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="18689-181">AlertTypeNumber</span></span> | <span data-ttu-id="18689-182">指定警示是否可以產生多個問題事件。</span><span class="sxs-lookup"><span data-stu-id="18689-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="18689-183">0 - 最新狀態。</span><span class="sxs-lookup"><span data-stu-id="18689-183">0 - State is up to date.</span></span><br><span data-ttu-id="18689-184">1 - 狀態未知。</span><span class="sxs-lookup"><span data-stu-id="18689-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="18689-185">註解</span><span class="sxs-lookup"><span data-stu-id="18689-185">Comments</span></span> | <span data-ttu-id="18689-186">警示的其他註解。</span><span class="sxs-lookup"><span data-stu-id="18689-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="18689-187">HostName</span><span class="sxs-lookup"><span data-stu-id="18689-187">HostName</span></span> | <span data-ttu-id="18689-188">建立警示的主機名稱。</span><span class="sxs-lookup"><span data-stu-id="18689-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="18689-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="18689-189">PriorityNumber</span></span> | <span data-ttu-id="18689-190">指出警示嚴重性的值。</span><span class="sxs-lookup"><span data-stu-id="18689-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="18689-191">0 - 未分類</span><span class="sxs-lookup"><span data-stu-id="18689-191">0 - not classified</span></span><br><span data-ttu-id="18689-192">1- 資訊</span><span class="sxs-lookup"><span data-stu-id="18689-192">1 - information</span></span><br><span data-ttu-id="18689-193">2 - 警告</span><span class="sxs-lookup"><span data-stu-id="18689-193">2 - warning</span></span><br><span data-ttu-id="18689-194">3 - 平均</span><span class="sxs-lookup"><span data-stu-id="18689-194">3 - average</span></span><br><span data-ttu-id="18689-195">4 - 高</span><span class="sxs-lookup"><span data-stu-id="18689-195">4 - high</span></span><br><span data-ttu-id="18689-196">5 - 嚴重損壞</span><span class="sxs-lookup"><span data-stu-id="18689-196">5 - disaster</span></span> |
| <span data-ttu-id="18689-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="18689-197">TimeGenerated</span></span> |<span data-ttu-id="18689-198">建立警示的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="18689-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="18689-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="18689-199">TimeLastModified</span></span> |<span data-ttu-id="18689-200">上次變更警示狀態的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="18689-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="18689-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18689-201">Next steps</span></span>
* <span data-ttu-id="18689-202">了解 Log Analytics 中的[警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="18689-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="18689-203">了解 [記錄搜尋](log-analytics-log-searches.md) ，其可分析從資料來源和方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="18689-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
