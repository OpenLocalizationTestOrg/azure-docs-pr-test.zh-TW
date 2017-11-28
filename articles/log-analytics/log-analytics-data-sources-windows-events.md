---
title: "收集與分析 OMS Log Analytics 中的 Windows 事件記錄檔 | Microsoft Docs"
description: "Windows 事件記錄檔是 Log Analytics 所使用的最常見資料來源之一。  本文說明如何設定收集 Windows 事件記錄檔，以及它們在 OMS 儲存機制中建立的記錄詳細資料。"
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
ms.openlocfilehash: 1be8500ec2cb78ef0edf57f4d8561336cf00ebcb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="windows-event-log-data-sources-in-log-analytics"></a><span data-ttu-id="f7805-104">Log Analytics 中的 Windows 事件記錄檔資料來源</span><span class="sxs-lookup"><span data-stu-id="f7805-104">Windows event log data sources in Log Analytics</span></span>
<span data-ttu-id="f7805-105">Windows 事件記錄檔是使用 Windows 代理程式收集資料的常見[資料來源](log-analytics-data-sources.md)之一，因為許多應用程式會寫入 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7805-105">Windows Event logs are one of the most common [data sources](log-analytics-data-sources.md) for collecting data using Windows agents since many applications write to the Windows event log.</span></span>  <span data-ttu-id="f7805-106">除了指定您要監視之應用程式所建立的任何自訂記錄檔之外，您也可以透過標準記錄檔 (例如系統和應用程式) 來收集事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-106">You can collect events from standard logs such as System and Application in addition to specifying any custom logs created by applications you need to monitor.</span></span>

![Windows 事件](media/log-analytics-data-sources-windows-events/overview.png)     

## <a name="configuring-windows-event-logs"></a><span data-ttu-id="f7805-108">設定 Windows 事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="f7805-108">Configuring Windows Event logs</span></span>
<span data-ttu-id="f7805-109">從 [Log Analytics [設定] 中的 [資料] 功能表](log-analytics-data-sources.md#configuring-data-sources)來設定 Windows 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7805-109">Configure Windows Event logs from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>

<span data-ttu-id="f7805-110">Log Analytics 只會從設定中指定的 Windows 事件記錄檔收集事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-110">Log Analytics only collects events from the Windows event logs that are specified in the settings.</span></span>  <span data-ttu-id="f7805-111">您可以輸入記錄檔的名稱，然後按一下 **+**，來新增事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f7805-111">You can add an event log by typing in the name of the log and clicking **+**.</span></span>  <span data-ttu-id="f7805-112">針對每個記錄檔，僅會收集包含所選嚴重性的事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-112">For each log, only the events with the selected severities are collected.</span></span>  <span data-ttu-id="f7805-113">請檢查您想要收集之特定記錄檔的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="f7805-113">Check the severities for the particular log that you want to collect.</span></span>  <span data-ttu-id="f7805-114">您無法提供任何其他準則來篩選事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-114">You cannot provide any additional criteria to filter events.</span></span>

<span data-ttu-id="f7805-115">輸入事件記錄檔的名稱時，Log Analytics 提供常見的事件記錄檔名稱的建議。</span><span class="sxs-lookup"><span data-stu-id="f7805-115">As you type the name of an event log, Log Analytics provides suggestions of common event log names.</span></span> <span data-ttu-id="f7805-116">如果您想要新增的記錄檔未出現在清單中，您仍然可以透過輸入記錄檔的完整名稱來新增它。</span><span class="sxs-lookup"><span data-stu-id="f7805-116">If the log you want to add does not appear in the list, you can still add it by typing in the full name of the log.</span></span> <span data-ttu-id="f7805-117">您可以使用事件檢視器來尋找記錄檔的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="f7805-117">You can find the full name of the log by using event viewer.</span></span> <span data-ttu-id="f7805-118">在事件檢視器中，開啟記錄檔的 [內容] 頁面，並從 [完整名稱] 欄位複製字串。</span><span class="sxs-lookup"><span data-stu-id="f7805-118">In event viewer, open the *Properties* page for the log and copy the string from the *Full Name* field.</span></span>

![設定 Windows 事件](media/log-analytics-data-sources-windows-events/configure.png)

## <a name="data-collection"></a><span data-ttu-id="f7805-120">資料收集</span><span class="sxs-lookup"><span data-stu-id="f7805-120">Data collection</span></span>
<span data-ttu-id="f7805-121">在建立事件時，Log Analytics 會從受監視的事件記錄檔收集符合所選嚴重性的每個事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-121">Log Analytics collects each event that matches a selected severity from a monitored event log as the event is created.</span></span>  <span data-ttu-id="f7805-122">代理程式會在它收集的每個事件記錄檔中記錄它的位置。</span><span class="sxs-lookup"><span data-stu-id="f7805-122">The agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="f7805-123">如果代理程式離線一段時間，Log Analytics 即會從上次停止的地方收集事件，即使這些事件是在代理程式離線時所建立亦同。</span><span class="sxs-lookup"><span data-stu-id="f7805-123">If the agent goes offline for a period of time, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.</span></span>  <span data-ttu-id="f7805-124">如果事件記錄檔是在代理程式離線時使用未收集且已遭覆寫的事件進行包裝，可能就無法收集這些事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-124">There is a potential for these events to not be collected if the event log wraps with uncollected events being overwritten while the agent is offline.</span></span>

>[!NOTE]
><span data-ttu-id="f7805-125">Log Analytics 不會收集 SQL Server 從 *MSSQLSERVER* 來源用含有關鍵字 - *Classic* 或 *Audit Success* 的事件 ID 18453 以及用關鍵字 *0xa0000000000000* 所建立的稽核事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-125">Log Analytics does not collect audit events created by SQL Server from source *MSSQLSERVER* with event ID 18453 that contains keywords - *Classic* or *Audit Success* and keyword *0xa0000000000000*.</span></span>
>

## <a name="windows-event-records-properties"></a><span data-ttu-id="f7805-126">Windows 事件記錄屬性</span><span class="sxs-lookup"><span data-stu-id="f7805-126">Windows event records properties</span></span>
<span data-ttu-id="f7805-127">Windows 事件記錄都具有 **Event** 類型以及下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="f7805-127">Windows event records have a type of **Event** and have the properties in the following table:</span></span>

| <span data-ttu-id="f7805-128">屬性</span><span class="sxs-lookup"><span data-stu-id="f7805-128">Property</span></span> | <span data-ttu-id="f7805-129">說明</span><span class="sxs-lookup"><span data-stu-id="f7805-129">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f7805-130">電腦</span><span class="sxs-lookup"><span data-stu-id="f7805-130">Computer</span></span> |<span data-ttu-id="f7805-131">收集事件的來源電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="f7805-131">Name of the computer that the event was collected from.</span></span> |
| <span data-ttu-id="f7805-132">EventCategory</span><span class="sxs-lookup"><span data-stu-id="f7805-132">EventCategory</span></span> |<span data-ttu-id="f7805-133">事件的類別。</span><span class="sxs-lookup"><span data-stu-id="f7805-133">Category of the event.</span></span> |
| <span data-ttu-id="f7805-134">EventData</span><span class="sxs-lookup"><span data-stu-id="f7805-134">EventData</span></span> |<span data-ttu-id="f7805-135">原始格式的所有事件資料。</span><span class="sxs-lookup"><span data-stu-id="f7805-135">All event data in raw format.</span></span> |
| <span data-ttu-id="f7805-136">EventID</span><span class="sxs-lookup"><span data-stu-id="f7805-136">EventID</span></span> |<span data-ttu-id="f7805-137">事件的編號。</span><span class="sxs-lookup"><span data-stu-id="f7805-137">Number of the event.</span></span> |
| <span data-ttu-id="f7805-138">EventLevel</span><span class="sxs-lookup"><span data-stu-id="f7805-138">EventLevel</span></span> |<span data-ttu-id="f7805-139">數值格式的事件嚴重性。</span><span class="sxs-lookup"><span data-stu-id="f7805-139">Severity of the event in numeric form.</span></span> |
| <span data-ttu-id="f7805-140">EventLevelName</span><span class="sxs-lookup"><span data-stu-id="f7805-140">EventLevelName</span></span> |<span data-ttu-id="f7805-141">文字格式的事件嚴重性。</span><span class="sxs-lookup"><span data-stu-id="f7805-141">Severity of the event in text form.</span></span> |
| <span data-ttu-id="f7805-142">EventLog</span><span class="sxs-lookup"><span data-stu-id="f7805-142">EventLog</span></span> |<span data-ttu-id="f7805-143">收集事件的來源事件記錄檔名稱。</span><span class="sxs-lookup"><span data-stu-id="f7805-143">Name of the event log that the event was collected from.</span></span> |
| <span data-ttu-id="f7805-144">ParameterXml</span><span class="sxs-lookup"><span data-stu-id="f7805-144">ParameterXml</span></span> |<span data-ttu-id="f7805-145">XML 格式的事件參數值。</span><span class="sxs-lookup"><span data-stu-id="f7805-145">Event parameter values in XML format.</span></span> |
| <span data-ttu-id="f7805-146">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="f7805-146">ManagementGroupName</span></span> |<span data-ttu-id="f7805-147">System Center Operations Manager 代理程式的管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="f7805-147">Name of the management group for System Center Operations Manager agents.</span></span>  <span data-ttu-id="f7805-148">若為其他代理程式，此值為 AOI-<workspace ID>。</span><span class="sxs-lookup"><span data-stu-id="f7805-148">For other agents, this value is AOI-<workspace ID></span></span> |
| <span data-ttu-id="f7805-149">RenderedDescription</span><span class="sxs-lookup"><span data-stu-id="f7805-149">RenderedDescription</span></span> |<span data-ttu-id="f7805-150">含參數值的事件描述</span><span class="sxs-lookup"><span data-stu-id="f7805-150">Event description with parameter values</span></span> |
| <span data-ttu-id="f7805-151">來源</span><span class="sxs-lookup"><span data-stu-id="f7805-151">Source</span></span> |<span data-ttu-id="f7805-152">事件的來源。</span><span class="sxs-lookup"><span data-stu-id="f7805-152">Source of the event.</span></span> |
| <span data-ttu-id="f7805-153">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="f7805-153">SourceSystem</span></span> |<span data-ttu-id="f7805-154">收集事件的來源代理程式類型。</span><span class="sxs-lookup"><span data-stu-id="f7805-154">Type of agent the event was collected from.</span></span> <br> <span data-ttu-id="f7805-155">OpsManager - Windows 代理程式，直接連接或由 Operations Manager 管理</span><span class="sxs-lookup"><span data-stu-id="f7805-155">OpsManager – Windows agent, either direct connect or Operations Manager managed</span></span> <br> <span data-ttu-id="f7805-156">Linux – 所有的 Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="f7805-156">Linux – All Linux agents</span></span>  <br> <span data-ttu-id="f7805-157">AzureStorage – Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="f7805-157">AzureStorage – Azure Diagnostics</span></span> |
| <span data-ttu-id="f7805-158">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="f7805-158">TimeGenerated</span></span> |<span data-ttu-id="f7805-159">在 Windows 中建立事件的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="f7805-159">Date and time the event was created in Windows.</span></span> |
| <span data-ttu-id="f7805-160">UserName</span><span class="sxs-lookup"><span data-stu-id="f7805-160">UserName</span></span> |<span data-ttu-id="f7805-161">記錄此事件之帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f7805-161">User name of the account that logged the event.</span></span> |

## <a name="log-searches-with-windows-events"></a><span data-ttu-id="f7805-162">使用 Windows 事件的記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="f7805-162">Log searches with Windows Events</span></span>
<span data-ttu-id="f7805-163">下表提供擷取 Windows 事件記錄的不同記錄搜尋範例。</span><span class="sxs-lookup"><span data-stu-id="f7805-163">The following table provides different examples of log searches that retrieve Windows Event records.</span></span>

| <span data-ttu-id="f7805-164">查詢</span><span class="sxs-lookup"><span data-stu-id="f7805-164">Query</span></span> | <span data-ttu-id="f7805-165">說明</span><span class="sxs-lookup"><span data-stu-id="f7805-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f7805-166">Type=Event</span><span class="sxs-lookup"><span data-stu-id="f7805-166">Type=Event</span></span> |<span data-ttu-id="f7805-167">所有的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-167">All Windows events.</span></span> |
| <span data-ttu-id="f7805-168">Type=Event EventLevelName=error</span><span class="sxs-lookup"><span data-stu-id="f7805-168">Type=Event EventLevelName=error</span></span> |<span data-ttu-id="f7805-169">所有 Windows 事件與錯誤的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="f7805-169">All Windows events with severity of error.</span></span> |
| <span data-ttu-id="f7805-170">Type=Event &#124; Measure count() by Source</span><span class="sxs-lookup"><span data-stu-id="f7805-170">Type=Event &#124; Measure count() by Source</span></span> |<span data-ttu-id="f7805-171">依據來源的 Windows 事件計數。</span><span class="sxs-lookup"><span data-stu-id="f7805-171">Count of Windows events by source.</span></span> |
| <span data-ttu-id="f7805-172">Type=Event EventLevelName=error &#124; Measure count() by Source</span><span class="sxs-lookup"><span data-stu-id="f7805-172">Type=Event EventLevelName=error &#124; Measure count() by Source</span></span> |<span data-ttu-id="f7805-173">依據來源的 Windows 錯誤事件計數。</span><span class="sxs-lookup"><span data-stu-id="f7805-173">Count of Windows error events by source.</span></span> |


>[!NOTE]
> <span data-ttu-id="f7805-174">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="f7805-174">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>
>
>| <span data-ttu-id="f7805-175">查詢</span><span class="sxs-lookup"><span data-stu-id="f7805-175">Query</span></span> | <span data-ttu-id="f7805-176">說明</span><span class="sxs-lookup"><span data-stu-id="f7805-176">Description</span></span> |
|:---|:---|
| <span data-ttu-id="f7805-177">Event</span><span class="sxs-lookup"><span data-stu-id="f7805-177">Event</span></span> |<span data-ttu-id="f7805-178">所有的 Windows 事件。</span><span class="sxs-lookup"><span data-stu-id="f7805-178">All Windows events.</span></span> |
| <span data-ttu-id="f7805-179">Event &#124; where EventLevelName == "error"</span><span class="sxs-lookup"><span data-stu-id="f7805-179">Event &#124; where EventLevelName == "error"</span></span> |<span data-ttu-id="f7805-180">所有 Windows 事件與錯誤的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="f7805-180">All Windows events with severity of error.</span></span> |
| <span data-ttu-id="f7805-181">Event &#124; summarize count() by Source</span><span class="sxs-lookup"><span data-stu-id="f7805-181">Event &#124; summarize count() by Source</span></span> |<span data-ttu-id="f7805-182">依據來源的 Windows 事件計數。</span><span class="sxs-lookup"><span data-stu-id="f7805-182">Count of Windows events by source.</span></span> |
| <span data-ttu-id="f7805-183">Event &#124; where EventLevelName == "error" &#124; summarize count() by Source</span><span class="sxs-lookup"><span data-stu-id="f7805-183">Event &#124; where EventLevelName == "error" &#124; summarize count() by Source</span></span> |<span data-ttu-id="f7805-184">依據來源的 Windows 錯誤事件計數。</span><span class="sxs-lookup"><span data-stu-id="f7805-184">Count of Windows error events by source.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="f7805-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7805-185">Next steps</span></span>
* <span data-ttu-id="f7805-186">設定 Log Analytics 以收集其他 [資料來源](log-analytics-data-sources.md) 進行分析。</span><span class="sxs-lookup"><span data-stu-id="f7805-186">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="f7805-187">了解 [記錄搜尋](log-analytics-log-searches.md) ，其可分析從資料來源和方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="f7805-187">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>  
* <span data-ttu-id="f7805-188">使用 [自訂欄位](log-analytics-custom-fields.md) ，以將事件記錄剖析至個別欄位。</span><span class="sxs-lookup"><span data-stu-id="f7805-188">Use [Custom Fields](log-analytics-custom-fields.md) to parse the event records into individual fields.</span></span>
* <span data-ttu-id="f7805-189">設定從您的 Windows 代理程式進行 [效能計數器收集](log-analytics-data-sources-performance-counters.md) 。</span><span class="sxs-lookup"><span data-stu-id="f7805-189">Configure [collection of performance counters](log-analytics-data-sources-performance-counters.md) from your Windows agents.</span></span>
