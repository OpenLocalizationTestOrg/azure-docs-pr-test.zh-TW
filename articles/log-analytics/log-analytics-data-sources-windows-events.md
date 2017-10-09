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
# <a name="windows-event-log-data-sources-in-log-analytics"></a><span data-ttu-id="0d540-104">Log Analytics 中的 Windows 事件記錄檔資料來源</span><span class="sxs-lookup"><span data-stu-id="0d540-104">Windows event log data sources in Log Analytics</span></span>
<span data-ttu-id="0d540-105">Windows 事件記錄檔是其中一種最常見的 hello[資料來源](log-analytics-data-sources.md)針對使用 Windows 代理程式，因為許多應用程式寫入 toohello Windows 事件記錄檔收集資料。</span><span class="sxs-lookup"><span data-stu-id="0d540-105">Windows Event logs are one of hello most common [data sources](log-analytics-data-sources.md) for collecting data using Windows agents since many applications write toohello Windows event log.</span></span>  <span data-ttu-id="0d540-106">您可以從收集事件中加入 toospecifying 在例如系統和應用程式的標準記錄檔建立的任何自訂記錄檔的應用程式中，您需要 toomonitor。</span><span class="sxs-lookup"><span data-stu-id="0d540-106">You can collect events from standard logs such as System and Application in addition toospecifying any custom logs created by applications you need toomonitor.</span></span>

![Windows 事件](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a><span data-ttu-id="0d540-108">設定 Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="0d540-108">Configuring Windows Event logs</span></span>
<span data-ttu-id="0d540-109">設定 Windows 事件記錄檔從 hello[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。</span><span class="sxs-lookup"><span data-stu-id="0d540-109">Configure Windows Event logs from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>

<span data-ttu-id="0d540-110">只記錄分析會從 hello hello 設定中指定的 Windows 事件記錄收集事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-110">Log Analytics only collects events from hello Windows event logs that are specified in hello settings.</span></span>  <span data-ttu-id="0d540-111">您可以將事件記錄檔加入 hello hello 記錄檔名稱中輸入，然後按一下 **+** 。</span><span class="sxs-lookup"><span data-stu-id="0d540-111">You can add an event log by typing in hello name of hello log and clicking **+**.</span></span>  <span data-ttu-id="0d540-112">針對每個記錄檔，會收集的 hello 事件只有與選取的 hello 嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0d540-112">For each log, only hello events with hello selected severities are collected.</span></span>  <span data-ttu-id="0d540-113">請檢查您想 toocollect hello 特定記錄檔的 hello 嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0d540-113">Check hello severities for hello particular log that you want toocollect.</span></span>  <span data-ttu-id="0d540-114">您無法提供任何其他準則 toofilter 事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-114">You cannot provide any additional criteria toofilter events.</span></span>

<span data-ttu-id="0d540-115">當您輸入 hello 事件記錄檔名稱時，記錄分析會提供的一般事件記錄檔名稱的建議。</span><span class="sxs-lookup"><span data-stu-id="0d540-115">As you type hello name of an event log, Log Analytics provides suggestions of common event log names.</span></span> <span data-ttu-id="0d540-116">如果您想要 tooadd hello 記錄 hello 清單中沒有出現，您仍然可以將它輸入 hello hello 記錄檔的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="0d540-116">If hello log you want tooadd does not appear in hello list, you can still add it by typing in hello full name of hello log.</span></span> <span data-ttu-id="0d540-117">您可以使用事件檢視器找到 hello hello 記錄檔的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="0d540-117">You can find hello full name of hello log by using event viewer.</span></span> <span data-ttu-id="0d540-118">在 事件檢視器中，開啟 hello*屬性*頁面 hello 記錄檔和複製 hello 字串 hello*全名*欄位。</span><span class="sxs-lookup"><span data-stu-id="0d540-118">In event viewer, open hello *Properties* page for hello log and copy hello string from hello *Full Name* field.</span></span>

![設定 Windows 事件](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a><span data-ttu-id="0d540-120">資料收集</span><span class="sxs-lookup"><span data-stu-id="0d540-120">Data collection</span></span>
<span data-ttu-id="0d540-121">記錄分析會收集每個事件都必須符合所選的嚴重性從受監視的事件記錄檔所建立 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-121">Log Analytics collects each event that matches a selected severity from a monitored event log as hello event is created.</span></span>  <span data-ttu-id="0d540-122">hello 代理程式會收集每個事件記錄檔中記錄其所在位置。</span><span class="sxs-lookup"><span data-stu-id="0d540-122">hello agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="0d540-123">如果 hello 代理程式離線一段時間，然後記錄分析會收集事件從上次停止的地方，即使這些事件在 hello agent 離線期間所建立。</span><span class="sxs-lookup"><span data-stu-id="0d540-123">If hello agent goes offline for a period of time, then Log Analytics collects events from where it last left off, even if those events were created while hello agent was offline.</span></span>  <span data-ttu-id="0d540-124">有可能會針對收集這些事件 toonot 若 hello 事件記錄檔會包裝與 hello 代理程式離線時遭到覆寫的回收事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-124">There is a potential for these events toonot be collected if hello event log wraps with uncollected events being overwritten while hello agent is offline.</span></span>

>[!NOTE]
><span data-ttu-id="0d540-125">Log Analytics 不會收集 SQL Server 從 *MSSQLSERVER* 來源用含有關鍵字 - *Classic* 或 *Audit Success* 的事件 ID 18453 以及用關鍵字 *0xa0000000000000* 所建立的稽核事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-125">Log Analytics does not collect audit events created by SQL Server from source *MSSQLSERVER* with event ID 18453 that contains keywords - *Classic* or *Audit Success* and keyword *0xa0000000000000*.</span></span>
>

## <a name="windows-event-records-properties"></a><span data-ttu-id="0d540-126">Windows 事件記錄屬性</span><span class="sxs-lookup"><span data-stu-id="0d540-126">Windows event records properties</span></span>
<span data-ttu-id="0d540-127">Windows 事件記錄都有一種**事件**和 hello 下表中都有 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="0d540-127">Windows event records have a type of **Event** and have hello properties in hello following table:</span></span>

| <span data-ttu-id="0d540-128">屬性</span><span class="sxs-lookup"><span data-stu-id="0d540-128">Property</span></span> | <span data-ttu-id="0d540-129">說明</span><span class="sxs-lookup"><span data-stu-id="0d540-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0d540-130">電腦</span><span class="sxs-lookup"><span data-stu-id="0d540-130">Computer</span></span> |<span data-ttu-id="0d540-131">從收集 hello hello 事件的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="0d540-131">Name of hello computer that hello event was collected from.</span></span> |
| <span data-ttu-id="0d540-132">EventCategory</span><span class="sxs-lookup"><span data-stu-id="0d540-132">EventCategory</span></span> |<span data-ttu-id="0d540-133">Hello 事件類別目錄。</span><span class="sxs-lookup"><span data-stu-id="0d540-133">Category of hello event.</span></span> |
| <span data-ttu-id="0d540-134">EventData</span><span class="sxs-lookup"><span data-stu-id="0d540-134">EventData</span></span> |<span data-ttu-id="0d540-135">原始格式的所有事件資料。</span><span class="sxs-lookup"><span data-stu-id="0d540-135">All event data in raw format.</span></span> |
| <span data-ttu-id="0d540-136">EventID</span><span class="sxs-lookup"><span data-stu-id="0d540-136">EventID</span></span> |<span data-ttu-id="0d540-137">Hello 事件數目。</span><span class="sxs-lookup"><span data-stu-id="0d540-137">Number of hello event.</span></span> |
| <span data-ttu-id="0d540-138">EventLevel</span><span class="sxs-lookup"><span data-stu-id="0d540-138">EventLevel</span></span> |<span data-ttu-id="0d540-139">數值格式中的 hello 事件的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0d540-139">Severity of hello event in numeric form.</span></span> |
| <span data-ttu-id="0d540-140">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="0d540-140">EventLevelName</span></span> |<span data-ttu-id="0d540-141">以文字格式的 hello 事件的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0d540-141">Severity of hello event in text form.</span></span> |
| <span data-ttu-id="0d540-142">EventLog</span><span class="sxs-lookup"><span data-stu-id="0d540-142">EventLog</span></span> |<span data-ttu-id="0d540-143">從收集 hello 事件 hello 事件記錄檔名稱。</span><span class="sxs-lookup"><span data-stu-id="0d540-143">Name of hello event log that hello event was collected from.</span></span> |
| <span data-ttu-id="0d540-144">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="0d540-144">ParameterXml</span></span> |<span data-ttu-id="0d540-145">XML 格式的事件參數值。</span><span class="sxs-lookup"><span data-stu-id="0d540-145">Event parameter values in XML format.</span></span> |
| <span data-ttu-id="0d540-146">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="0d540-146">ManagementGroupName</span></span> |<span data-ttu-id="0d540-147">System Center Operations Manager 代理程式 hello 管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="0d540-147">Name of hello management group for System Center Operations Manager agents.</span></span>  <span data-ttu-id="0d540-148">若為其他代理程式，此值為 AOI-<workspace ID>。</span><span class="sxs-lookup"><span data-stu-id="0d540-148">For other agents, this value is AOI-<workspace ID></span></span> |
| <span data-ttu-id="0d540-149">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="0d540-149">RenderedDescription</span></span> |<span data-ttu-id="0d540-150">含參數值的事件描述</span><span class="sxs-lookup"><span data-stu-id="0d540-150">Event description with parameter values</span></span> |
| <span data-ttu-id="0d540-151">來源</span><span class="sxs-lookup"><span data-stu-id="0d540-151">Source</span></span> |<span data-ttu-id="0d540-152">Hello 事件的來源。</span><span class="sxs-lookup"><span data-stu-id="0d540-152">Source of hello event.</span></span> |
| <span data-ttu-id="0d540-153">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="0d540-153">SourceSystem</span></span> |<span data-ttu-id="0d540-154">從已收集的代理程式 hello 事件類型。</span><span class="sxs-lookup"><span data-stu-id="0d540-154">Type of agent hello event was collected from.</span></span> <br> <span data-ttu-id="0d540-155">OpsManager - Windows 代理程式，直接連接或由 Operations Manager 管理</span><span class="sxs-lookup"><span data-stu-id="0d540-155">OpsManager – Windows agent, either direct connect or Operations Manager managed</span></span> <br> <span data-ttu-id="0d540-156">Linux – 所有的 Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="0d540-156">Linux – All Linux agents</span></span>  <br> <span data-ttu-id="0d540-157">AzureStorage – Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="0d540-157">AzureStorage – Azure Diagnostics</span></span> |
| <span data-ttu-id="0d540-158">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="0d540-158">TimeGenerated</span></span> |<span data-ttu-id="0d540-159">在 Windows 中，已建立日期和時間的 hello 事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-159">Date and time hello event was created in Windows.</span></span> |
| <span data-ttu-id="0d540-160">UserName</span><span class="sxs-lookup"><span data-stu-id="0d540-160">UserName</span></span> |<span data-ttu-id="0d540-161">記錄 hello 事件 hello 帳戶使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0d540-161">User name of hello account that logged hello event.</span></span> |

## <a name="log-searches-with-windows-events"></a><span data-ttu-id="0d540-162">使用 Windows 事件的記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="0d540-162">Log searches with Windows Events</span></span>
<span data-ttu-id="0d540-163">hello 下表提供不同範例擷取 Windows 事件記錄的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="0d540-163">hello following table provides different examples of log searches that retrieve Windows Event records.</span></span>

| <span data-ttu-id="0d540-164">查詢</span><span class="sxs-lookup"><span data-stu-id="0d540-164">Query</span></span> | <span data-ttu-id="0d540-165">說明</span><span class="sxs-lookup"><span data-stu-id="0d540-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0d540-166">Type=Event</span><span class="sxs-lookup"><span data-stu-id="0d540-166">Type=Event</span></span> |<span data-ttu-id="0d540-167">所有的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-167">All Windows events.</span></span> |
| <span data-ttu-id="0d540-168">Type=Event EventLevelName=error</span><span class="sxs-lookup"><span data-stu-id="0d540-168">Type=Event EventLevelName=error</span></span> |<span data-ttu-id="0d540-169">所有 Windows 事件與錯誤的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0d540-169">All Windows events with severity of error.</span></span> |
| <span data-ttu-id="0d540-170">Type=Event &#124; Measure count() by Source</span><span class="sxs-lookup"><span data-stu-id="0d540-170">Type=Event &#124; Measure count() by Source</span></span> |<span data-ttu-id="0d540-171">依據來源的 Windows 事件計數。</span><span class="sxs-lookup"><span data-stu-id="0d540-171">Count of Windows events by source.</span></span> |
| <span data-ttu-id="0d540-172">Type=Event EventLevelName=error &#124; Measure count() by Source</span><span class="sxs-lookup"><span data-stu-id="0d540-172">Type=Event EventLevelName=error &#124; Measure count() by Source</span></span> |<span data-ttu-id="0d540-173">依據來源的 Windows 錯誤事件計數。</span><span class="sxs-lookup"><span data-stu-id="0d540-173">Count of Windows error events by source.</span></span> |


>[!NOTE]
> <span data-ttu-id="0d540-174">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="0d540-174">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>
>
>| <span data-ttu-id="0d540-175">查詢</span><span class="sxs-lookup"><span data-stu-id="0d540-175">Query</span></span> | <span data-ttu-id="0d540-176">說明</span><span class="sxs-lookup"><span data-stu-id="0d540-176">Description</span></span> |
|:---|:---|
| <span data-ttu-id="0d540-177">Event</span><span class="sxs-lookup"><span data-stu-id="0d540-177">Event</span></span> |<span data-ttu-id="0d540-178">所有的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="0d540-178">All Windows events.</span></span> |
| <span data-ttu-id="0d540-179">Event &#124; where EventLevelName == "error"</span><span class="sxs-lookup"><span data-stu-id="0d540-179">Event &#124; where EventLevelName == "error"</span></span> |<span data-ttu-id="0d540-180">所有 Windows 事件與錯誤的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="0d540-180">All Windows events with severity of error.</span></span> |
| <span data-ttu-id="0d540-181">Event &#124; summarize count() by Source</span><span class="sxs-lookup"><span data-stu-id="0d540-181">Event &#124; summarize count() by Source</span></span> |<span data-ttu-id="0d540-182">依據來源的 Windows 事件計數。</span><span class="sxs-lookup"><span data-stu-id="0d540-182">Count of Windows events by source.</span></span> |
| <span data-ttu-id="0d540-183">Event &#124; where EventLevelName == "error" &#124; summarize count() by Source</span><span class="sxs-lookup"><span data-stu-id="0d540-183">Event &#124; where EventLevelName == "error" &#124; summarize count() by Source</span></span> |<span data-ttu-id="0d540-184">依據來源的 Windows 錯誤事件計數。</span><span class="sxs-lookup"><span data-stu-id="0d540-184">Count of Windows error events by source.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0d540-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d540-185">Next steps</span></span>
* <span data-ttu-id="0d540-186">設定記錄分析 toocollect 其他[資料來源](log-analytics-data-sources.md)進行分析。</span><span class="sxs-lookup"><span data-stu-id="0d540-186">Configure Log Analytics toocollect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="0d540-187">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="0d540-187">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>  
* <span data-ttu-id="0d540-188">使用[自訂欄位](log-analytics-custom-fields.md)tooparse hello 事件記錄，到個別的欄位。</span><span class="sxs-lookup"><span data-stu-id="0d540-188">Use [Custom Fields](log-analytics-custom-fields.md) tooparse hello event records into individual fields.</span></span>
* <span data-ttu-id="0d540-189">設定從您的 Windows 代理程式進行 [效能計數器收集](log-analytics-data-sources-performance-counters.md) 。</span><span class="sxs-lookup"><span data-stu-id="0d540-189">Configure [collection of performance counters](log-analytics-data-sources-performance-counters.md) from your Windows agents.</span></span>
