---
title: "Log Analytics 中的 IIS 記錄檔 | Microsoft Docs"
description: "Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。  本文說明如何設定收集 IIS 記錄檔，以及它們在 OMS 儲存機制中建立的記錄詳細資料。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: cec5ff0a-01f5-4262-b2e8-e3db7b7467d2
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: bwren
ms.openlocfilehash: 2114bdafb3b9fe2eb0632271840b8b70a76d10f1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="iis-logs-in-log-analytics"></a><span data-ttu-id="988b8-104">Log Analytics 中的 IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="988b8-104">IIS logs in Log Analytics</span></span>
<span data-ttu-id="988b8-105">Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。</span><span class="sxs-lookup"><span data-stu-id="988b8-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span></span>  

![IIS 記錄檔](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a><span data-ttu-id="988b8-107">設定 IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="988b8-107">Configuring IIS logs</span></span>
<span data-ttu-id="988b8-108">Log Analytics 會從 IIS 建立的記錄檔收集項目，因此您必須[設定 IIS 記錄](https://technet.microsoft.com/library/hh831775.aspx)。</span><span class="sxs-lookup"><span data-stu-id="988b8-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span></span>

<span data-ttu-id="988b8-109">Log Analytics 只支援以 W3C 格式儲存的 IIS 記錄檔，不支援自訂欄位或 IIS 進階記錄。</span><span class="sxs-lookup"><span data-stu-id="988b8-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span></span>  
<span data-ttu-id="988b8-110">Log Analytics 不會收集 NCSA 或 IIS 原生格式的記錄。</span><span class="sxs-lookup"><span data-stu-id="988b8-110">Log Analytics does not collect logs in NCSA or IIS native format.</span></span>

<span data-ttu-id="988b8-111">從 [Log Analytics [設定] 中的 [資料] 功能表](log-analytics-data-sources.md#configuring-data-sources)來設定 Log Analytics 中的 IIS 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="988b8-111">Configure IIS logs in Log Analytics from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="988b8-112">您只需選取 [Collect W3C format IIS log files]\(收集 W3C 格式的 IIS 記錄檔) 即可完成設定。</span><span class="sxs-lookup"><span data-stu-id="988b8-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span></span>

<span data-ttu-id="988b8-113">當您啟用 IIS 記錄檔收集時，建議您在每部伺服器上設定 IIS 記錄檔換用設定。</span><span class="sxs-lookup"><span data-stu-id="988b8-113">We recommend that when you enable IIS log collection, you should configure the IIS log rollover setting on each server.</span></span>

## <a name="data-collection"></a><span data-ttu-id="988b8-114">資料收集</span><span class="sxs-lookup"><span data-stu-id="988b8-114">Data collection</span></span>
<span data-ttu-id="988b8-115">Log Analytics 會從每個連接的來源收集 IIS 記錄檔項目，間隔大約為每 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="988b8-115">Log Analytics collects IIS log entries from each connected source approximately every 15 minutes.</span></span>  <span data-ttu-id="988b8-116">代理程式會在它收集的每個事件記錄檔中記錄它的位置。</span><span class="sxs-lookup"><span data-stu-id="988b8-116">The agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="988b8-117">如果代理程式離線，Log Analytics 會從上次離開的地方收集事件，即使這些事件是在代理程式離線時所建立亦同。</span><span class="sxs-lookup"><span data-stu-id="988b8-117">If the agent goes offline, then Log Analytics collects events from where it last left off, even if those events were created while the agent was offline.</span></span>

## <a name="iis-log-record-properties"></a><span data-ttu-id="988b8-118">IIS 記錄檔記錄屬性</span><span class="sxs-lookup"><span data-stu-id="988b8-118">IIS log record properties</span></span>
<span data-ttu-id="988b8-119">IIS 記錄檔記錄都具有 **W3CIISLog** 類型以及下表中的屬性：</span><span class="sxs-lookup"><span data-stu-id="988b8-119">IIS log records have a type of **W3CIISLog** and have the properties in the following table:</span></span>

| <span data-ttu-id="988b8-120">屬性</span><span class="sxs-lookup"><span data-stu-id="988b8-120">Property</span></span> | <span data-ttu-id="988b8-121">說明</span><span class="sxs-lookup"><span data-stu-id="988b8-121">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="988b8-122">電腦</span><span class="sxs-lookup"><span data-stu-id="988b8-122">Computer</span></span> |<span data-ttu-id="988b8-123">收集事件的來源電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="988b8-123">Name of the computer that the event was collected from.</span></span> |
| <span data-ttu-id="988b8-124">cIP</span><span class="sxs-lookup"><span data-stu-id="988b8-124">cIP</span></span> |<span data-ttu-id="988b8-125">用戶端的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="988b8-125">IP address of the client.</span></span> |
| <span data-ttu-id="988b8-126">csMethod</span><span class="sxs-lookup"><span data-stu-id="988b8-126">csMethod</span></span> |<span data-ttu-id="988b8-127">要求的方法，例如 GET 或 POST。</span><span class="sxs-lookup"><span data-stu-id="988b8-127">Method of the request such as GET or POST.</span></span> |
| <span data-ttu-id="988b8-128">csReferer</span><span class="sxs-lookup"><span data-stu-id="988b8-128">csReferer</span></span> |<span data-ttu-id="988b8-129">使用者連結至目前網站的來源網站。</span><span class="sxs-lookup"><span data-stu-id="988b8-129">Site that the user followed a link from to the current site.</span></span> |
| <span data-ttu-id="988b8-130">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="988b8-130">csUserAgent</span></span> |<span data-ttu-id="988b8-131">用戶端的瀏覽器類型。</span><span class="sxs-lookup"><span data-stu-id="988b8-131">Browser type of the client.</span></span> |
| <span data-ttu-id="988b8-132">csUserName</span><span class="sxs-lookup"><span data-stu-id="988b8-132">csUserName</span></span> |<span data-ttu-id="988b8-133">存取伺服器之已驗證的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="988b8-133">Name of the authenticated user that accessed the server.</span></span> <span data-ttu-id="988b8-134">匿名使用者會以連字號表示。</span><span class="sxs-lookup"><span data-stu-id="988b8-134">Anonymous users are indicated by a hyphen.</span></span> |
| <span data-ttu-id="988b8-135">csUriStem</span><span class="sxs-lookup"><span data-stu-id="988b8-135">csUriStem</span></span> |<span data-ttu-id="988b8-136">要求的目標，例如網頁。</span><span class="sxs-lookup"><span data-stu-id="988b8-136">Target of the request such as a web page.</span></span> |
| <span data-ttu-id="988b8-137">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="988b8-137">csUriQuery</span></span> |<span data-ttu-id="988b8-138">用戶端正在嘗試執行的查詢 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="988b8-138">Query, if any, that the client was trying to perform.</span></span> |
| <span data-ttu-id="988b8-139">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="988b8-139">ManagementGroupName</span></span> |<span data-ttu-id="988b8-140">Operations Manager 代理程式的管理群組名稱。</span><span class="sxs-lookup"><span data-stu-id="988b8-140">Name of the management group for Operations Manager agents.</span></span>  <span data-ttu-id="988b8-141">若為其他代理程式，此為 AOI-\<工作區 ID\></span><span class="sxs-lookup"><span data-stu-id="988b8-141">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="988b8-142">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="988b8-142">RemoteIPCountry</span></span> |<span data-ttu-id="988b8-143">用戶端 IP 位址的國家/地區。</span><span class="sxs-lookup"><span data-stu-id="988b8-143">Country of the IP address of the client.</span></span> |
| <span data-ttu-id="988b8-144">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="988b8-144">RemoteIPLatitude</span></span> |<span data-ttu-id="988b8-145">用戶端 IP 位址的緯度。</span><span class="sxs-lookup"><span data-stu-id="988b8-145">Latitude of the client IP address.</span></span> |
| <span data-ttu-id="988b8-146">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="988b8-146">RemoteIPLongitude</span></span> |<span data-ttu-id="988b8-147">用戶端 IP 位址的經度。</span><span class="sxs-lookup"><span data-stu-id="988b8-147">Longitude of the client IP address.</span></span> |
| <span data-ttu-id="988b8-148">scStatus</span><span class="sxs-lookup"><span data-stu-id="988b8-148">scStatus</span></span> |<span data-ttu-id="988b8-149">HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="988b8-149">HTTP status code.</span></span> |
| <span data-ttu-id="988b8-150">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="988b8-150">scSubStatus</span></span> |<span data-ttu-id="988b8-151">子狀態錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="988b8-151">Substatus error code.</span></span> |
| <span data-ttu-id="988b8-152">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="988b8-152">scWin32Status</span></span> |<span data-ttu-id="988b8-153">Windows 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="988b8-153">Windows status code.</span></span> |
| <span data-ttu-id="988b8-154">sIP</span><span class="sxs-lookup"><span data-stu-id="988b8-154">sIP</span></span> |<span data-ttu-id="988b8-155">Web 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="988b8-155">IP address of the web server.</span></span> |
| <span data-ttu-id="988b8-156">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="988b8-156">SourceSystem</span></span> |<span data-ttu-id="988b8-157">OpsMgr</span><span class="sxs-lookup"><span data-stu-id="988b8-157">OpsMgr</span></span> |
| <span data-ttu-id="988b8-158">sPort</span><span class="sxs-lookup"><span data-stu-id="988b8-158">sPort</span></span> |<span data-ttu-id="988b8-159">用戶端連接之伺服器上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="988b8-159">Port on the server the client connected to.</span></span> |
| <span data-ttu-id="988b8-160">sSiteName</span><span class="sxs-lookup"><span data-stu-id="988b8-160">sSiteName</span></span> |<span data-ttu-id="988b8-161">IIS 網站名稱。</span><span class="sxs-lookup"><span data-stu-id="988b8-161">Name of the IIS site.</span></span> |
| <span data-ttu-id="988b8-162">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="988b8-162">TimeGenerated</span></span> |<span data-ttu-id="988b8-163">記錄項目的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="988b8-163">Date and time the entry was logged.</span></span> |
| <span data-ttu-id="988b8-164">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="988b8-164">TimeTaken</span></span> |<span data-ttu-id="988b8-165">處理要求的時間長度 (以毫秒為單位)。</span><span class="sxs-lookup"><span data-stu-id="988b8-165">Length of time to process the request in milliseconds.</span></span> |

## <a name="log-searches-with-iis-logs"></a><span data-ttu-id="988b8-166">使用 IIS 記錄檔的記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="988b8-166">Log searches with IIS logs</span></span>
<span data-ttu-id="988b8-167">下表提供擷取 IIS 記錄檔記錄的不同記錄查詢範例。</span><span class="sxs-lookup"><span data-stu-id="988b8-167">The following table provides different examples of log queries that retrieve IIS log records.</span></span>

| <span data-ttu-id="988b8-168">查詢</span><span class="sxs-lookup"><span data-stu-id="988b8-168">Query</span></span> | <span data-ttu-id="988b8-169">說明</span><span class="sxs-lookup"><span data-stu-id="988b8-169">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="988b8-170">Type=W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="988b8-170">Type=W3CIISLog</span></span> |<span data-ttu-id="988b8-171">所有 IIS 記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="988b8-171">All IIS log records.</span></span> |
| <span data-ttu-id="988b8-172">Type=W3CIISLog scStatus=500</span><span class="sxs-lookup"><span data-stu-id="988b8-172">Type=W3CIISLog scStatus=500</span></span> |<span data-ttu-id="988b8-173">具有傳回狀態 500 的所有 IIS 記錄。</span><span class="sxs-lookup"><span data-stu-id="988b8-173">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="988b8-174">Type=W3CIISLog &#124; Measure count() by cIP</span><span class="sxs-lookup"><span data-stu-id="988b8-174">Type=W3CIISLog &#124; Measure count() by cIP</span></span> |<span data-ttu-id="988b8-175">依據用戶端 IP 位址的 IIS 記錄項目計數。</span><span class="sxs-lookup"><span data-stu-id="988b8-175">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="988b8-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="988b8-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span></span> |<span data-ttu-id="988b8-177">依據主機 www.contoso.com 之 URL 的 IIS 記錄項目計數。</span><span class="sxs-lookup"><span data-stu-id="988b8-177">Count of IIS log entries by URL for the host www.contoso.com.</span></span> |
| <span data-ttu-id="988b8-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span><span class="sxs-lookup"><span data-stu-id="988b8-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span></span> |<span data-ttu-id="988b8-179">每部 IIS 電腦所接收的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="988b8-179">Total bytes received by each IIS computer.</span></span> |

>[!NOTE]
> <span data-ttu-id="988b8-180">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="988b8-180">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="988b8-181">查詢</span><span class="sxs-lookup"><span data-stu-id="988b8-181">Query</span></span> | <span data-ttu-id="988b8-182">說明</span><span class="sxs-lookup"><span data-stu-id="988b8-182">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="988b8-183">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="988b8-183">W3CIISLog</span></span> |<span data-ttu-id="988b8-184">所有 IIS 記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="988b8-184">All IIS log records.</span></span> |
| <span data-ttu-id="988b8-185">W3CIISLog &#124; where scStatus==500</span><span class="sxs-lookup"><span data-stu-id="988b8-185">W3CIISLog &#124; where scStatus==500</span></span> |<span data-ttu-id="988b8-186">具有傳回狀態 500 的所有 IIS 記錄。</span><span class="sxs-lookup"><span data-stu-id="988b8-186">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="988b8-187">W3CIISLog &#124; summarize count() by cIP</span><span class="sxs-lookup"><span data-stu-id="988b8-187">W3CIISLog &#124; summarize count() by cIP</span></span> |<span data-ttu-id="988b8-188">依據用戶端 IP 位址的 IIS 記錄項目計數。</span><span class="sxs-lookup"><span data-stu-id="988b8-188">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="988b8-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="988b8-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span></span> |<span data-ttu-id="988b8-190">依據主機 www.contoso.com 之 URL 的 IIS 記錄項目計數。</span><span class="sxs-lookup"><span data-stu-id="988b8-190">Count of IIS log entries by URL for the host www.contoso.com.</span></span> |
| <span data-ttu-id="988b8-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span><span class="sxs-lookup"><span data-stu-id="988b8-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span></span> |<span data-ttu-id="988b8-192">每部 IIS 電腦所接收的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="988b8-192">Total bytes received by each IIS computer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="988b8-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="988b8-193">Next steps</span></span>
* <span data-ttu-id="988b8-194">設定 Log Analytics 以收集其他 [資料來源](log-analytics-data-sources.md) 進行分析。</span><span class="sxs-lookup"><span data-stu-id="988b8-194">Configure Log Analytics to collect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="988b8-195">了解 [記錄檔搜尋](log-analytics-log-searches.md) ，其可分析從資料來源和方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="988b8-195">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="988b8-196">設定 Log Analytics 中的警示，以主動通知您在 IIS 記錄檔中找到的重要狀況。</span><span class="sxs-lookup"><span data-stu-id="988b8-196">Configure alerts in Log Analytics to proactively notify you of important conditions found in IIS logs.</span></span>
