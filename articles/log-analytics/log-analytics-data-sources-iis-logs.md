---
title: "記錄中記錄分析的 aaaIIS |Microsoft 文件"
description: "Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。  這篇文章描述如何 tooconfigure 收集 IIS 記錄檔和詳細資料的 hello 記錄它們建立 hello OMS 儲存機制中。"
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
ms.openlocfilehash: c5575351090cdabaf651bcb49867794ee3a4b6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="iis-logs-in-log-analytics"></a><span data-ttu-id="ace1a-104">Log Analytics 中的 IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="ace1a-104">IIS logs in Log Analytics</span></span>
<span data-ttu-id="ace1a-105">Internet Information Services (IIS) 會將使用者活動儲存在記錄檔中，並可由 Log Analytics 進行收集。</span><span class="sxs-lookup"><span data-stu-id="ace1a-105">Internet Information Services (IIS) stores user activity in log files that can be collected by Log Analytics.</span></span>  

![IIS 記錄檔](media/log-analytics-data-sources-iis-logs/overview.png)

## <a name="configuring-iis-logs"></a><span data-ttu-id="ace1a-107">設定 IIS 記錄檔</span><span class="sxs-lookup"><span data-stu-id="ace1a-107">Configuring IIS logs</span></span>
<span data-ttu-id="ace1a-108">Log Analytics 會從 IIS 建立的記錄檔收集項目，因此您必須[設定 IIS 記錄](https://technet.microsoft.com/library/hh831775.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ace1a-108">Log Analytics collects entries from log files created by IIS, so you must [configure IIS for logging](https://technet.microsoft.com/library/hh831775.aspx).</span></span>

<span data-ttu-id="ace1a-109">Log Analytics 只支援以 W3C 格式儲存的 IIS 記錄檔，不支援自訂欄位或 IIS 進階記錄。</span><span class="sxs-lookup"><span data-stu-id="ace1a-109">Log Analytics only supports IIS log files stored in W3C format and does not support custom fields or IIS Advanced Logging.</span></span>  
<span data-ttu-id="ace1a-110">Log Analytics 不會收集 NCSA 或 IIS 原生格式的記錄。</span><span class="sxs-lookup"><span data-stu-id="ace1a-110">Log Analytics does not collect logs in NCSA or IIS native format.</span></span>

<span data-ttu-id="ace1a-111">設定 IIS 記錄檔中記錄分析，從 hello[資料記錄分析設定 功能表](log-analytics-data-sources.md#configuring-data-sources)。</span><span class="sxs-lookup"><span data-stu-id="ace1a-111">Configure IIS logs in Log Analytics from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="ace1a-112">您只需選取 [Collect W3C format IIS log files]\(收集 W3C 格式的 IIS 記錄檔) 即可完成設定。</span><span class="sxs-lookup"><span data-stu-id="ace1a-112">There is no configuration required other than selecting **Collect W3C format IIS log files**.</span></span>

<span data-ttu-id="ace1a-113">我們建議，當您啟用 IIS 記錄檔集合，您應該 hello IIS 記錄檔變換 設定每部伺服器上設定。</span><span class="sxs-lookup"><span data-stu-id="ace1a-113">We recommend that when you enable IIS log collection, you should configure hello IIS log rollover setting on each server.</span></span>

## <a name="data-collection"></a><span data-ttu-id="ace1a-114">資料收集</span><span class="sxs-lookup"><span data-stu-id="ace1a-114">Data collection</span></span>
<span data-ttu-id="ace1a-115">Log Analytics 會從每個連接的來源收集 IIS 記錄檔項目，間隔大約為每 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="ace1a-115">Log Analytics collects IIS log entries from each connected source approximately every 15 minutes.</span></span>  <span data-ttu-id="ace1a-116">hello 代理程式會收集每個事件記錄檔中記錄其所在位置。</span><span class="sxs-lookup"><span data-stu-id="ace1a-116">hello agent records its place in each event log that it collects from.</span></span>  <span data-ttu-id="ace1a-117">如果 hello 代理程式離線，然後記錄分析會收集事件從上次停止的地方，即使這些事件在 hello agent 離線期間所建立。</span><span class="sxs-lookup"><span data-stu-id="ace1a-117">If hello agent goes offline, then Log Analytics collects events from where it last left off, even if those events were created while hello agent was offline.</span></span>

## <a name="iis-log-record-properties"></a><span data-ttu-id="ace1a-118">IIS 記錄檔記錄屬性</span><span class="sxs-lookup"><span data-stu-id="ace1a-118">IIS log record properties</span></span>
<span data-ttu-id="ace1a-119">IIS 記錄檔記錄有一種**W3CIISLog**和 hello 下表中都有 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="ace1a-119">IIS log records have a type of **W3CIISLog** and have hello properties in hello following table:</span></span>

| <span data-ttu-id="ace1a-120">屬性</span><span class="sxs-lookup"><span data-stu-id="ace1a-120">Property</span></span> | <span data-ttu-id="ace1a-121">說明</span><span class="sxs-lookup"><span data-stu-id="ace1a-121">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ace1a-122">電腦</span><span class="sxs-lookup"><span data-stu-id="ace1a-122">Computer</span></span> |<span data-ttu-id="ace1a-123">從收集 hello hello 事件的電腦名稱。</span><span class="sxs-lookup"><span data-stu-id="ace1a-123">Name of hello computer that hello event was collected from.</span></span> |
| <span data-ttu-id="ace1a-124">cIP</span><span class="sxs-lookup"><span data-stu-id="ace1a-124">cIP</span></span> |<span data-ttu-id="ace1a-125">Hello 用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ace1a-125">IP address of hello client.</span></span> |
| <span data-ttu-id="ace1a-126">csMethod</span><span class="sxs-lookup"><span data-stu-id="ace1a-126">csMethod</span></span> |<span data-ttu-id="ace1a-127">Hello 要求，例如 GET 或 POST 方法。</span><span class="sxs-lookup"><span data-stu-id="ace1a-127">Method of hello request such as GET or POST.</span></span> |
| <span data-ttu-id="ace1a-128">csReferer</span><span class="sxs-lookup"><span data-stu-id="ace1a-128">csReferer</span></span> |<span data-ttu-id="ace1a-129">站台的 hello 使用者接著再從 toohello 目前網站的連結。</span><span class="sxs-lookup"><span data-stu-id="ace1a-129">Site that hello user followed a link from toohello current site.</span></span> |
| <span data-ttu-id="ace1a-130">csUserAgent</span><span class="sxs-lookup"><span data-stu-id="ace1a-130">csUserAgent</span></span> |<span data-ttu-id="ace1a-131">Hello 用戶端瀏覽器類型。</span><span class="sxs-lookup"><span data-stu-id="ace1a-131">Browser type of hello client.</span></span> |
| <span data-ttu-id="ace1a-132">csUserName</span><span class="sxs-lookup"><span data-stu-id="ace1a-132">csUserName</span></span> |<span data-ttu-id="ace1a-133">Hello 名稱驗證的使用者存取 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ace1a-133">Name of hello authenticated user that accessed hello server.</span></span> <span data-ttu-id="ace1a-134">匿名使用者會以連字號表示。</span><span class="sxs-lookup"><span data-stu-id="ace1a-134">Anonymous users are indicated by a hyphen.</span></span> |
| <span data-ttu-id="ace1a-135">csUriStem</span><span class="sxs-lookup"><span data-stu-id="ace1a-135">csUriStem</span></span> |<span data-ttu-id="ace1a-136">例如，網頁的 hello 要求的目標。</span><span class="sxs-lookup"><span data-stu-id="ace1a-136">Target of hello request such as a web page.</span></span> |
| <span data-ttu-id="ace1a-137">csUriQuery</span><span class="sxs-lookup"><span data-stu-id="ace1a-137">csUriQuery</span></span> |<span data-ttu-id="ace1a-138">查詢中，如果有的話，該 hello 用戶端已嘗試 tooperform。</span><span class="sxs-lookup"><span data-stu-id="ace1a-138">Query, if any, that hello client was trying tooperform.</span></span> |
| <span data-ttu-id="ace1a-139">ManagementGroupName</span><span class="sxs-lookup"><span data-stu-id="ace1a-139">ManagementGroupName</span></span> |<span data-ttu-id="ace1a-140">Hello 管理群組的 Operations Manager 代理程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="ace1a-140">Name of hello management group for Operations Manager agents.</span></span>  <span data-ttu-id="ace1a-141">若為其他代理程式，此為 AOI-\<工作區 ID\></span><span class="sxs-lookup"><span data-stu-id="ace1a-141">For other agents, this is AOI-\<workspace ID\></span></span> |
| <span data-ttu-id="ace1a-142">RemoteIPCountry</span><span class="sxs-lookup"><span data-stu-id="ace1a-142">RemoteIPCountry</span></span> |<span data-ttu-id="ace1a-143">國家/地區的 hello hello 用戶端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ace1a-143">Country of hello IP address of hello client.</span></span> |
| <span data-ttu-id="ace1a-144">RemoteIPLatitude</span><span class="sxs-lookup"><span data-stu-id="ace1a-144">RemoteIPLatitude</span></span> |<span data-ttu-id="ace1a-145">Hello 用戶端 IP 位址的緯度。</span><span class="sxs-lookup"><span data-stu-id="ace1a-145">Latitude of hello client IP address.</span></span> |
| <span data-ttu-id="ace1a-146">RemoteIPLongitude</span><span class="sxs-lookup"><span data-stu-id="ace1a-146">RemoteIPLongitude</span></span> |<span data-ttu-id="ace1a-147">Hello 用戶端 IP 位址的經度。</span><span class="sxs-lookup"><span data-stu-id="ace1a-147">Longitude of hello client IP address.</span></span> |
| <span data-ttu-id="ace1a-148">scStatus</span><span class="sxs-lookup"><span data-stu-id="ace1a-148">scStatus</span></span> |<span data-ttu-id="ace1a-149">HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ace1a-149">HTTP status code.</span></span> |
| <span data-ttu-id="ace1a-150">scSubStatus</span><span class="sxs-lookup"><span data-stu-id="ace1a-150">scSubStatus</span></span> |<span data-ttu-id="ace1a-151">子狀態錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="ace1a-151">Substatus error code.</span></span> |
| <span data-ttu-id="ace1a-152">scWin32Status</span><span class="sxs-lookup"><span data-stu-id="ace1a-152">scWin32Status</span></span> |<span data-ttu-id="ace1a-153">Windows 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="ace1a-153">Windows status code.</span></span> |
| <span data-ttu-id="ace1a-154">sIP</span><span class="sxs-lookup"><span data-stu-id="ace1a-154">sIP</span></span> |<span data-ttu-id="ace1a-155">Hello web 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ace1a-155">IP address of hello web server.</span></span> |
| <span data-ttu-id="ace1a-156">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ace1a-156">SourceSystem</span></span> |<span data-ttu-id="ace1a-157">OpsMgr</span><span class="sxs-lookup"><span data-stu-id="ace1a-157">OpsMgr</span></span> |
| <span data-ttu-id="ace1a-158">sPort</span><span class="sxs-lookup"><span data-stu-id="ace1a-158">sPort</span></span> |<span data-ttu-id="ace1a-159">Hello 伺服器 hello 用戶端上的連接埠連接到。</span><span class="sxs-lookup"><span data-stu-id="ace1a-159">Port on hello server hello client connected to.</span></span> |
| <span data-ttu-id="ace1a-160">sSiteName</span><span class="sxs-lookup"><span data-stu-id="ace1a-160">sSiteName</span></span> |<span data-ttu-id="ace1a-161">Hello IIS 站台名稱。</span><span class="sxs-lookup"><span data-stu-id="ace1a-161">Name of hello IIS site.</span></span> |
| <span data-ttu-id="ace1a-162">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ace1a-162">TimeGenerated</span></span> |<span data-ttu-id="ace1a-163">已記錄的日期和時間的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="ace1a-163">Date and time hello entry was logged.</span></span> |
| <span data-ttu-id="ace1a-164">TimeTaken</span><span class="sxs-lookup"><span data-stu-id="ace1a-164">TimeTaken</span></span> |<span data-ttu-id="ace1a-165">以毫秒為單位，要求的時間 tooprocess hello 長度。</span><span class="sxs-lookup"><span data-stu-id="ace1a-165">Length of time tooprocess hello request in milliseconds.</span></span> |

## <a name="log-searches-with-iis-logs"></a><span data-ttu-id="ace1a-166">使用 IIS 記錄檔的記錄搜尋</span><span class="sxs-lookup"><span data-stu-id="ace1a-166">Log searches with IIS logs</span></span>
<span data-ttu-id="ace1a-167">hello 下表提供不同的擷取 IIS 記錄檔記錄的記錄檔查詢的範例。</span><span class="sxs-lookup"><span data-stu-id="ace1a-167">hello following table provides different examples of log queries that retrieve IIS log records.</span></span>

| <span data-ttu-id="ace1a-168">查詢</span><span class="sxs-lookup"><span data-stu-id="ace1a-168">Query</span></span> | <span data-ttu-id="ace1a-169">說明</span><span class="sxs-lookup"><span data-stu-id="ace1a-169">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ace1a-170">Type=W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ace1a-170">Type=W3CIISLog</span></span> |<span data-ttu-id="ace1a-171">所有 IIS 記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="ace1a-171">All IIS log records.</span></span> |
| <span data-ttu-id="ace1a-172">Type=W3CIISLog scStatus=500</span><span class="sxs-lookup"><span data-stu-id="ace1a-172">Type=W3CIISLog scStatus=500</span></span> |<span data-ttu-id="ace1a-173">具有傳回狀態 500 的所有 IIS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ace1a-173">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="ace1a-174">Type=W3CIISLog &#124; Measure count() by cIP</span><span class="sxs-lookup"><span data-stu-id="ace1a-174">Type=W3CIISLog &#124; Measure count() by cIP</span></span> |<span data-ttu-id="ace1a-175">依據用戶端 IP 位址的 IIS 記錄項目計數。</span><span class="sxs-lookup"><span data-stu-id="ace1a-175">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="ace1a-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="ace1a-176">Type=W3CIISLog csHost="www.contoso.com" &#124; Measure count() by csUriStem</span></span> |<span data-ttu-id="ace1a-177">計數的 IIS 記錄 url hello 主機 www.contoso.com 的項目。</span><span class="sxs-lookup"><span data-stu-id="ace1a-177">Count of IIS log entries by URL for hello host www.contoso.com.</span></span> |
| <span data-ttu-id="ace1a-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span><span class="sxs-lookup"><span data-stu-id="ace1a-178">Type=W3CIISLog &#124; Measure Sum(csBytes) by Computer &#124; top 500000</span></span> |<span data-ttu-id="ace1a-179">每部 IIS 電腦所接收的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="ace1a-179">Total bytes received by each IIS computer.</span></span> |

>[!NOTE]
> <span data-ttu-id="ace1a-180">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="ace1a-180">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="ace1a-181">查詢</span><span class="sxs-lookup"><span data-stu-id="ace1a-181">Query</span></span> | <span data-ttu-id="ace1a-182">說明</span><span class="sxs-lookup"><span data-stu-id="ace1a-182">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ace1a-183">W3CIISLog</span><span class="sxs-lookup"><span data-stu-id="ace1a-183">W3CIISLog</span></span> |<span data-ttu-id="ace1a-184">所有 IIS 記錄檔記錄。</span><span class="sxs-lookup"><span data-stu-id="ace1a-184">All IIS log records.</span></span> |
| <span data-ttu-id="ace1a-185">W3CIISLog &#124; where scStatus==500</span><span class="sxs-lookup"><span data-stu-id="ace1a-185">W3CIISLog &#124; where scStatus==500</span></span> |<span data-ttu-id="ace1a-186">具有傳回狀態 500 的所有 IIS 記錄。</span><span class="sxs-lookup"><span data-stu-id="ace1a-186">All IIS log records with a return status of 500.</span></span> |
| <span data-ttu-id="ace1a-187">W3CIISLog &#124; summarize count() by cIP</span><span class="sxs-lookup"><span data-stu-id="ace1a-187">W3CIISLog &#124; summarize count() by cIP</span></span> |<span data-ttu-id="ace1a-188">依據用戶端 IP 位址的 IIS 記錄項目計數。</span><span class="sxs-lookup"><span data-stu-id="ace1a-188">Count of IIS log entries by client IP address.</span></span> |
| <span data-ttu-id="ace1a-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span><span class="sxs-lookup"><span data-stu-id="ace1a-189">W3CIISLog &#124; where csHost=="www.contoso.com" &#124; summarize count() by csUriStem</span></span> |<span data-ttu-id="ace1a-190">計數的 IIS 記錄 url hello 主機 www.contoso.com 的項目。</span><span class="sxs-lookup"><span data-stu-id="ace1a-190">Count of IIS log entries by URL for hello host www.contoso.com.</span></span> |
| <span data-ttu-id="ace1a-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span><span class="sxs-lookup"><span data-stu-id="ace1a-191">W3CIISLog &#124; summarize sum(csBytes) by Computer &#124; take 500000</span></span> |<span data-ttu-id="ace1a-192">每部 IIS 電腦所接收的位元組總數。</span><span class="sxs-lookup"><span data-stu-id="ace1a-192">Total bytes received by each IIS computer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ace1a-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ace1a-193">Next steps</span></span>
* <span data-ttu-id="ace1a-194">設定記錄分析 toocollect 其他[資料來源](log-analytics-data-sources.md)進行分析。</span><span class="sxs-lookup"><span data-stu-id="ace1a-194">Configure Log Analytics toocollect other [data sources](log-analytics-data-sources.md) for analysis.</span></span>
* <span data-ttu-id="ace1a-195">深入了解[記錄搜尋](log-analytics-log-searches.md)tooanalyze hello 資料收集的資料來源和解決方案。</span><span class="sxs-lookup"><span data-stu-id="ace1a-195">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="ace1a-196">設定警示 tooproactively 通知您重要的條件，IIS 記錄檔中找到的記錄分析中。</span><span class="sxs-lookup"><span data-stu-id="ace1a-196">Configure alerts in Log Analytics tooproactively notify you of important conditions found in IIS logs.</span></span>
