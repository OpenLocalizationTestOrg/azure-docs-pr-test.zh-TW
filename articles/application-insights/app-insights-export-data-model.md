---
title: "Azure Application Insights 資料模型 | Microsoft Docs"
description: "描述從 JSON 中的連續匯出匯出的屬性，並做為篩選器。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: cabad41c-0518-4669-887f-3087aef865ea
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/21/2016
ms.author: bwren
ms.openlocfilehash: a485ddd555f65473d81896effc4a3562bda71410
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="3395b-103">Application Insights 匯出資料模型</span><span class="sxs-lookup"><span data-stu-id="3395b-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="3395b-104">此表列出從 [Application Insights](app-insights-overview.md) SDK 傳送至入口網站的遙測屬性。</span><span class="sxs-lookup"><span data-stu-id="3395b-104">This table lists the properties of telemetry sent from the [Application Insights](app-insights-overview.md) SDKs to the portal.</span></span>
<span data-ttu-id="3395b-105">您會在 [連續匯出](app-insights-export-telemetry.md)的資料輸出中看到這些屬性。</span><span class="sxs-lookup"><span data-stu-id="3395b-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="3395b-106">它們也會出現在[計量瀏覽器](app-insights-metrics-explorer.md)和[診斷搜尋](app-insights-diagnostic-search.md)的屬性篩選中。</span><span class="sxs-lookup"><span data-stu-id="3395b-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="3395b-107">注意事項：</span><span class="sxs-lookup"><span data-stu-id="3395b-107">Points to note:</span></span>

* <span data-ttu-id="3395b-108">`[0]` 代表您必須在路徑中插入索引的一點，但它未必是 0。</span><span class="sxs-lookup"><span data-stu-id="3395b-108">`[0]` in these tables denotes a point in the path where you have to insert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="3395b-109">持續時間的長度單位是微秒，因此 10000000 == 1 秒。</span><span class="sxs-lookup"><span data-stu-id="3395b-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="3395b-110">日期和時間是 UTC，並以 ISO 格式 `yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="3395b-110">Dates and times are UTC, and are given in the ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="3395b-111">範例</span><span class="sxs-lookup"><span data-stu-id="3395b-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent to client
        "success": true, // Default == responseCode<400
        // Request id becomes the operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently the following fields are redundant:
          "count": 1.0,
          "min": 1046804.0,
          "max": 1046804.0,
          "stdDev": 0.0,
          "sampledValue": 1046804.0
        },
        "url": "/"
      }
    ],
    "internal": {
      "data": {
        "id": "7f156650-ef4c-11e5-8453-3f984b167d05",
        "documentVersion": "1.61"
      }
    },
    "context": {
      "device": { // client browser
        "type": "PC",
        "screenResolution": { },
        "roleInstance": "WFWEB14B.fabrikam.net"
      },
      "application": { },
      "location": { // derived from client ip
        "continent": "North America",
        "country": "United States",
        // last octagon is anonymized to 0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent to portal:
        "samplingRate": 100.0,
        "eventTime": "2016-03-21T10:05:45.7334717Z" // UTC
      },
      "user": {
        "isAuthenticated": false,
        "anonId": "us-tx-sn1-azr", // bot agent id
        "anonAcquisitionDate": "0001-01-01T00:00:00Z",
        "authAcquisitionDate": "0001-01-01T00:00:00Z",
        "accountAcquisitionDate": "0001-01-01T00:00:00Z"
      },
      "operation": {
        "id": "fCOhCdCnZ9I=",
        "parentId": "fCOhCdCnZ9I=",
        "name": "GET Home/Index"
      },
      "cloud": { },
      "serverDevice": { },
      "custom": { // set by custom fields of track calls
        "dimensions": [ ],
        "metrics": [ ]
      },
      "session": {
        "id": "65504c10-44a6-489e-b9dc-94184eb00d86",
        "isFirst": true
      }
    }
  <span data-ttu-id="3395b-112">}</span><span class="sxs-lookup"><span data-stu-id="3395b-112">}</span></span>

## <a name="context"></a><span data-ttu-id="3395b-113">Context</span><span class="sxs-lookup"><span data-stu-id="3395b-113">Context</span></span>
<span data-ttu-id="3395b-114">所有類型的遙測都會伴隨內容區段。</span><span class="sxs-lookup"><span data-stu-id="3395b-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="3395b-115">並非所有的欄位都會連同每個資料點傳輸。</span><span class="sxs-lookup"><span data-stu-id="3395b-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="3395b-116">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-116">Path</span></span> | <span data-ttu-id="3395b-117">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-117">Type</span></span> | <span data-ttu-id="3395b-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="3395b-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="3395b-120">物件 [ ]</span><span class="sxs-lookup"><span data-stu-id="3395b-120">object [ ]</span></span> |<span data-ttu-id="3395b-121">由自訂屬性參數設定的索引鍵-值字串組。</span><span class="sxs-lookup"><span data-stu-id="3395b-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="3395b-122">索引鍵的最大長度 100，值的最大長度 1024。</span><span class="sxs-lookup"><span data-stu-id="3395b-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="3395b-123">超過 100 個唯一值時，屬性可供搜尋，但無法用來分割。</span><span class="sxs-lookup"><span data-stu-id="3395b-123">More than 100 unique values, the property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="3395b-124">每個 ikey 的最大值 200 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="3395b-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="3395b-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="3395b-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="3395b-126">物件 [ ]</span><span class="sxs-lookup"><span data-stu-id="3395b-126">object [ ]</span></span> |<span data-ttu-id="3395b-127">由自訂測量參數和 TrackMetrics 設定的索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="3395b-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="3395b-128">索引鍵的最大長度 100，值可能為數值。</span><span class="sxs-lookup"><span data-stu-id="3395b-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="3395b-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="3395b-129">context.data.eventTime</span></span> |<span data-ttu-id="3395b-130">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-130">string</span></span> |<span data-ttu-id="3395b-131">UTC</span><span class="sxs-lookup"><span data-stu-id="3395b-131">UTC</span></span> |
| <span data-ttu-id="3395b-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="3395b-132">context.data.isSynthetic</span></span> |<span data-ttu-id="3395b-133">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-133">boolean</span></span> |<span data-ttu-id="3395b-134">要求似乎來自 bot 或 web 測試。</span><span class="sxs-lookup"><span data-stu-id="3395b-134">Request appears to come from a bot or web test.</span></span> |
| <span data-ttu-id="3395b-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="3395b-135">context.data.samplingRate</span></span> |<span data-ttu-id="3395b-136">number</span><span class="sxs-lookup"><span data-stu-id="3395b-136">number</span></span> |<span data-ttu-id="3395b-137">由傳送至入口網站之 SDK 所產生的遙測百分比。</span><span class="sxs-lookup"><span data-stu-id="3395b-137">Percentage of telemetry generated by the SDK that is sent to portal.</span></span> <span data-ttu-id="3395b-138">範圍 0.0-100.0。</span><span class="sxs-lookup"><span data-stu-id="3395b-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="3395b-139">context.device</span><span class="sxs-lookup"><span data-stu-id="3395b-139">context.device</span></span> |<span data-ttu-id="3395b-140">物件</span><span class="sxs-lookup"><span data-stu-id="3395b-140">object</span></span> |<span data-ttu-id="3395b-141">用戶端裝置</span><span class="sxs-lookup"><span data-stu-id="3395b-141">Client device</span></span> |
| <span data-ttu-id="3395b-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="3395b-142">context.device.browser</span></span> |<span data-ttu-id="3395b-143">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-143">string</span></span> |<span data-ttu-id="3395b-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="3395b-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="3395b-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="3395b-145">context.device.browserVersion</span></span> |<span data-ttu-id="3395b-146">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-146">string</span></span> |<span data-ttu-id="3395b-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="3395b-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="3395b-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="3395b-148">context.device.deviceModel</span></span> |<span data-ttu-id="3395b-149">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-149">string</span></span> | |
| <span data-ttu-id="3395b-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="3395b-150">context.device.deviceName</span></span> |<span data-ttu-id="3395b-151">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-151">string</span></span> | |
| <span data-ttu-id="3395b-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="3395b-152">context.device.id</span></span> |<span data-ttu-id="3395b-153">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-153">string</span></span> | |
| <span data-ttu-id="3395b-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="3395b-154">context.device.locale</span></span> |<span data-ttu-id="3395b-155">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-155">string</span></span> |<span data-ttu-id="3395b-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="3395b-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="3395b-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="3395b-157">context.device.network</span></span> |<span data-ttu-id="3395b-158">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-158">string</span></span> | |
| <span data-ttu-id="3395b-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="3395b-159">context.device.oemName</span></span> |<span data-ttu-id="3395b-160">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-160">string</span></span> | |
| <span data-ttu-id="3395b-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="3395b-161">context.device.osVersion</span></span> |<span data-ttu-id="3395b-162">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-162">string</span></span> |<span data-ttu-id="3395b-163">主機作業系統</span><span class="sxs-lookup"><span data-stu-id="3395b-163">Host OS</span></span> |
| <span data-ttu-id="3395b-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="3395b-164">context.device.roleInstance</span></span> |<span data-ttu-id="3395b-165">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-165">string</span></span> |<span data-ttu-id="3395b-166">伺服器主機的識別碼</span><span class="sxs-lookup"><span data-stu-id="3395b-166">ID of server host</span></span> |
| <span data-ttu-id="3395b-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="3395b-167">context.device.roleName</span></span> |<span data-ttu-id="3395b-168">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-168">string</span></span> | |
| <span data-ttu-id="3395b-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="3395b-169">context.device.type</span></span> |<span data-ttu-id="3395b-170">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-170">string</span></span> |<span data-ttu-id="3395b-171">PC, Browser, ...</span><span class="sxs-lookup"><span data-stu-id="3395b-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="3395b-172">context.location</span><span class="sxs-lookup"><span data-stu-id="3395b-172">context.location</span></span> |<span data-ttu-id="3395b-173">物件</span><span class="sxs-lookup"><span data-stu-id="3395b-173">object</span></span> |<span data-ttu-id="3395b-174">衍生自 clientip。</span><span class="sxs-lookup"><span data-stu-id="3395b-174">Derived from clientip.</span></span> |
| <span data-ttu-id="3395b-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="3395b-175">context.location.city</span></span> |<span data-ttu-id="3395b-176">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-176">string</span></span> |<span data-ttu-id="3395b-177">衍生自 clientip (如果已知)</span><span class="sxs-lookup"><span data-stu-id="3395b-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="3395b-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="3395b-178">context.location.clientip</span></span> |<span data-ttu-id="3395b-179">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-179">string</span></span> |<span data-ttu-id="3395b-180">最後一個八邊形匿名設定為 0。</span><span class="sxs-lookup"><span data-stu-id="3395b-180">Last octagon is anonymized to 0.</span></span> |
| <span data-ttu-id="3395b-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="3395b-181">context.location.continent</span></span> |<span data-ttu-id="3395b-182">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-182">string</span></span> | |
| <span data-ttu-id="3395b-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="3395b-183">context.location.country</span></span> |<span data-ttu-id="3395b-184">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-184">string</span></span> | |
| <span data-ttu-id="3395b-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="3395b-185">context.location.province</span></span> |<span data-ttu-id="3395b-186">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-186">string</span></span> |<span data-ttu-id="3395b-187">州或省</span><span class="sxs-lookup"><span data-stu-id="3395b-187">State or province</span></span> |
| <span data-ttu-id="3395b-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="3395b-188">context.operation.id</span></span> |<span data-ttu-id="3395b-189">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-189">string</span></span> |<span data-ttu-id="3395b-190">具有相同作業識別碼的項目會在入口網站中顯示為相關項目。</span><span class="sxs-lookup"><span data-stu-id="3395b-190">Items that have the same operation id are shown as Related Items in the portal.</span></span> <span data-ttu-id="3395b-191">通常為要求 id。</span><span class="sxs-lookup"><span data-stu-id="3395b-191">Usually the request id.</span></span> |
| <span data-ttu-id="3395b-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="3395b-192">context.operation.name</span></span> |<span data-ttu-id="3395b-193">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-193">string</span></span> |<span data-ttu-id="3395b-194">url 或要求名稱</span><span class="sxs-lookup"><span data-stu-id="3395b-194">url or request name</span></span> |
| <span data-ttu-id="3395b-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="3395b-195">context.operation.parentId</span></span> |<span data-ttu-id="3395b-196">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-196">string</span></span> |<span data-ttu-id="3395b-197">允許巢狀的相關項目。</span><span class="sxs-lookup"><span data-stu-id="3395b-197">Allows nested related items.</span></span> |
| <span data-ttu-id="3395b-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="3395b-198">context.session.id</span></span> |<span data-ttu-id="3395b-199">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-199">string</span></span> |<span data-ttu-id="3395b-200">來自相同來源的作業群組識別碼。</span><span class="sxs-lookup"><span data-stu-id="3395b-200">Id of a group of operations from the same source.</span></span> <span data-ttu-id="3395b-201">在 30 分鐘期間沒有發出工作階段結束訊號的作業。</span><span class="sxs-lookup"><span data-stu-id="3395b-201">A period of 30 minutes without an operation signals the end of a session.</span></span> |
| <span data-ttu-id="3395b-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="3395b-202">context.session.isFirst</span></span> |<span data-ttu-id="3395b-203">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-203">boolean</span></span> | |
| <span data-ttu-id="3395b-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="3395b-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="3395b-205">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-205">string</span></span> | |
| <span data-ttu-id="3395b-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="3395b-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="3395b-207">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-207">string</span></span> | |
| <span data-ttu-id="3395b-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="3395b-208">context.user.anonId</span></span> |<span data-ttu-id="3395b-209">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-209">string</span></span> | |
| <span data-ttu-id="3395b-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="3395b-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="3395b-211">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-211">string</span></span> |[<span data-ttu-id="3395b-212">已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="3395b-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="3395b-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="3395b-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="3395b-214">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-214">boolean</span></span> | |
| <span data-ttu-id="3395b-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="3395b-215">internal.data.documentVersion</span></span> |<span data-ttu-id="3395b-216">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-216">string</span></span> | |
| <span data-ttu-id="3395b-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="3395b-217">internal.data.id</span></span> |<span data-ttu-id="3395b-218">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="3395b-219">事件</span><span class="sxs-lookup"><span data-stu-id="3395b-219">Events</span></span>
<span data-ttu-id="3395b-220">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)產生的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="3395b-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="3395b-221">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-221">Path</span></span> | <span data-ttu-id="3395b-222">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-222">Type</span></span> | <span data-ttu-id="3395b-223">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-224">事件 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="3395b-224">event [0] count</span></span> |<span data-ttu-id="3395b-225">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-225">integer</span></span> |<span data-ttu-id="3395b-226">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="3395b-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="3395b-227">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="3395b-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="3395b-228">事件 [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="3395b-228">event [0] name</span></span> |<span data-ttu-id="3395b-229">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-229">string</span></span> |<span data-ttu-id="3395b-230">事件名稱。</span><span class="sxs-lookup"><span data-stu-id="3395b-230">Event name.</span></span>  <span data-ttu-id="3395b-231">最大長度 250。</span><span class="sxs-lookup"><span data-stu-id="3395b-231">Max length 250.</span></span> |
| <span data-ttu-id="3395b-232">事件 [0] url</span><span class="sxs-lookup"><span data-stu-id="3395b-232">event [0] url</span></span> |<span data-ttu-id="3395b-233">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-233">string</span></span> | |
| <span data-ttu-id="3395b-234">事件 [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="3395b-234">event [0] urlData.base</span></span> |<span data-ttu-id="3395b-235">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-235">string</span></span> | |
| <span data-ttu-id="3395b-236">事件 [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="3395b-236">event [0] urlData.host</span></span> |<span data-ttu-id="3395b-237">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="3395b-238">例外狀況</span><span class="sxs-lookup"><span data-stu-id="3395b-238">Exceptions</span></span>
<span data-ttu-id="3395b-239">回報在伺服器和瀏覽器中的 [例外狀況](app-insights-asp-net-exceptions.md) 。</span><span class="sxs-lookup"><span data-stu-id="3395b-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in the server and in the browser.</span></span>

| <span data-ttu-id="3395b-240">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-240">Path</span></span> | <span data-ttu-id="3395b-241">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-241">Type</span></span> | <span data-ttu-id="3395b-242">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-243">basicException [0] 組件</span><span class="sxs-lookup"><span data-stu-id="3395b-243">basicException [0] assembly</span></span> |<span data-ttu-id="3395b-244">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-244">string</span></span> | |
| <span data-ttu-id="3395b-245">basicException [0] 計數</span><span class="sxs-lookup"><span data-stu-id="3395b-245">basicException [0] count</span></span> |<span data-ttu-id="3395b-246">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-246">integer</span></span> |<span data-ttu-id="3395b-247">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="3395b-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="3395b-248">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="3395b-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="3395b-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="3395b-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="3395b-250">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-250">string</span></span> | |
| <span data-ttu-id="3395b-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="3395b-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="3395b-252">string</span><span class="sxs-lookup"><span data-stu-id="3395b-252">string</span></span> | |
| <span data-ttu-id="3395b-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="3395b-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="3395b-254">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-254">string</span></span> | |
| <span data-ttu-id="3395b-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="3395b-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="3395b-256">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-256">string</span></span> | |
| <span data-ttu-id="3395b-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="3395b-257">basicException [0] handledAt</span></span> |<span data-ttu-id="3395b-258">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-258">string</span></span> | |
| <span data-ttu-id="3395b-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="3395b-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="3395b-260">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-260">boolean</span></span> | |
| <span data-ttu-id="3395b-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="3395b-261">basicException [0] id</span></span> |<span data-ttu-id="3395b-262">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-262">string</span></span> | |
| <span data-ttu-id="3395b-263">basicException [0] 方法</span><span class="sxs-lookup"><span data-stu-id="3395b-263">basicException [0] method</span></span> |<span data-ttu-id="3395b-264">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-264">string</span></span> | |
| <span data-ttu-id="3395b-265">basicException [0] 訊息</span><span class="sxs-lookup"><span data-stu-id="3395b-265">basicException [0] message</span></span> |<span data-ttu-id="3395b-266">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-266">string</span></span> |<span data-ttu-id="3395b-267">例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="3395b-267">Exception message.</span></span> <span data-ttu-id="3395b-268">最大長度 10k。</span><span class="sxs-lookup"><span data-stu-id="3395b-268">Max length 10k.</span></span> |
| <span data-ttu-id="3395b-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="3395b-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="3395b-270">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-270">string</span></span> | |
| <span data-ttu-id="3395b-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="3395b-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="3395b-272">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-272">string</span></span> | |
| <span data-ttu-id="3395b-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="3395b-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="3395b-274">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-274">string</span></span> | |
| <span data-ttu-id="3395b-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="3395b-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="3395b-276">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-276">string</span></span> | |
| <span data-ttu-id="3395b-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="3395b-277">basicException [0] outerId</span></span> |<span data-ttu-id="3395b-278">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-278">string</span></span> | |
| <span data-ttu-id="3395b-279">basicException [0] parsedStack [0] 組件</span><span class="sxs-lookup"><span data-stu-id="3395b-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="3395b-280">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-280">string</span></span> | |
| <span data-ttu-id="3395b-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="3395b-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="3395b-282">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-282">string</span></span> | |
| <span data-ttu-id="3395b-283">basicException [0] parsedStack [0] 層級</span><span class="sxs-lookup"><span data-stu-id="3395b-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="3395b-284">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-284">integer</span></span> | |
| <span data-ttu-id="3395b-285">basicException [0] parsedStack [0] 列</span><span class="sxs-lookup"><span data-stu-id="3395b-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="3395b-286">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-286">integer</span></span> | |
| <span data-ttu-id="3395b-287">basicException [0] parsedStack [0] 方法</span><span class="sxs-lookup"><span data-stu-id="3395b-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="3395b-288">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-288">string</span></span> | |
| <span data-ttu-id="3395b-289">basicException [0] 堆疊</span><span class="sxs-lookup"><span data-stu-id="3395b-289">basicException [0] stack</span></span> |<span data-ttu-id="3395b-290">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-290">string</span></span> |<span data-ttu-id="3395b-291">最大長度 10k</span><span class="sxs-lookup"><span data-stu-id="3395b-291">Max length 10k</span></span> |
| <span data-ttu-id="3395b-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="3395b-292">basicException [0] typeName</span></span> |<span data-ttu-id="3395b-293">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="3395b-294">追蹤訊息</span><span class="sxs-lookup"><span data-stu-id="3395b-294">Trace Messages</span></span>
<span data-ttu-id="3395b-295">由 [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace) 及[記錄配接器](app-insights-asp-net-trace-logs.md)傳送。</span><span class="sxs-lookup"><span data-stu-id="3395b-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by the [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="3395b-296">路徑</span><span class="sxs-lookup"><span data-stu-id="3395b-296">Path</span></span> | <span data-ttu-id="3395b-297">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-297">Type</span></span> | <span data-ttu-id="3395b-298">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-299">訊息 [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="3395b-299">message [0] loggerName</span></span> |<span data-ttu-id="3395b-300">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-300">string</span></span> | |
| <span data-ttu-id="3395b-301">訊息 [0] 參數</span><span class="sxs-lookup"><span data-stu-id="3395b-301">message [0] parameters</span></span> |<span data-ttu-id="3395b-302">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-302">string</span></span> | |
| <span data-ttu-id="3395b-303">訊息 [0] 原始碼</span><span class="sxs-lookup"><span data-stu-id="3395b-303">message [0] raw</span></span> |<span data-ttu-id="3395b-304">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-304">string</span></span> |<span data-ttu-id="3395b-305">記錄檔訊息，最大長度 10k。</span><span class="sxs-lookup"><span data-stu-id="3395b-305">The log message, max length 10k.</span></span> |
| <span data-ttu-id="3395b-306">訊息 [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="3395b-306">message [0] severityLevel</span></span> |<span data-ttu-id="3395b-307">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="3395b-308">遠端相依性</span><span class="sxs-lookup"><span data-stu-id="3395b-308">Remote dependency</span></span>
<span data-ttu-id="3395b-309">由 TrackDependency 傳送。</span><span class="sxs-lookup"><span data-stu-id="3395b-309">Sent by TrackDependency.</span></span> <span data-ttu-id="3395b-310">用於回報伺服器中 [相依性呼叫](app-insights-asp-net-dependencies.md) 以及瀏覽器中 AJAX 呼叫的效能和使用情形。</span><span class="sxs-lookup"><span data-stu-id="3395b-310">Used to report performance and usage of [calls to dependencies](app-insights-asp-net-dependencies.md) in the server, and AJAX calls in the browser.</span></span>

| <span data-ttu-id="3395b-311">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-311">Path</span></span> | <span data-ttu-id="3395b-312">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-312">Type</span></span> | <span data-ttu-id="3395b-313">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="3395b-314">remoteDependency [0] async</span></span> |<span data-ttu-id="3395b-315">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-315">boolean</span></span> | |
| <span data-ttu-id="3395b-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="3395b-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="3395b-317">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-317">string</span></span> | |
| <span data-ttu-id="3395b-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="3395b-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="3395b-319">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-319">string</span></span> |<span data-ttu-id="3395b-320">例如 "home/index"</span><span class="sxs-lookup"><span data-stu-id="3395b-320">For example "home/index"</span></span> |
| <span data-ttu-id="3395b-321">remoteDependency [0] 計數</span><span class="sxs-lookup"><span data-stu-id="3395b-321">remoteDependency [0] count</span></span> |<span data-ttu-id="3395b-322">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-322">integer</span></span> |<span data-ttu-id="3395b-323">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="3395b-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="3395b-324">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="3395b-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="3395b-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="3395b-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="3395b-326">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-326">string</span></span> |<span data-ttu-id="3395b-327">HTTP、SQL、...</span><span class="sxs-lookup"><span data-stu-id="3395b-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="3395b-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="3395b-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="3395b-329">number</span><span class="sxs-lookup"><span data-stu-id="3395b-329">number</span></span> |<span data-ttu-id="3395b-330">從根據相依性呼叫回應完成開始計算的時間</span><span class="sxs-lookup"><span data-stu-id="3395b-330">Time from call to completion of response by dependency</span></span> |
| <span data-ttu-id="3395b-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="3395b-331">remoteDependency [0] id</span></span> |<span data-ttu-id="3395b-332">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-332">string</span></span> | |
| <span data-ttu-id="3395b-333">remoteDependency [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="3395b-333">remoteDependency [0] name</span></span> |<span data-ttu-id="3395b-334">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-334">string</span></span> |<span data-ttu-id="3395b-335">Url。</span><span class="sxs-lookup"><span data-stu-id="3395b-335">Url.</span></span> <span data-ttu-id="3395b-336">最大長度 250。</span><span class="sxs-lookup"><span data-stu-id="3395b-336">Max length 250.</span></span> |
| <span data-ttu-id="3395b-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="3395b-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="3395b-338">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-338">string</span></span> |<span data-ttu-id="3395b-339">從 HTTP 相依性</span><span class="sxs-lookup"><span data-stu-id="3395b-339">from HTTP dependency</span></span> |
| <span data-ttu-id="3395b-340">remoteDependency [0] 成功</span><span class="sxs-lookup"><span data-stu-id="3395b-340">remoteDependency [0] success</span></span> |<span data-ttu-id="3395b-341">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-341">boolean</span></span> | |
| <span data-ttu-id="3395b-342">remoteDependency [0] 類型</span><span class="sxs-lookup"><span data-stu-id="3395b-342">remoteDependency [0] type</span></span> |<span data-ttu-id="3395b-343">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-343">string</span></span> |<span data-ttu-id="3395b-344">Http、Sql、...</span><span class="sxs-lookup"><span data-stu-id="3395b-344">Http, Sql,...</span></span> |
| <span data-ttu-id="3395b-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="3395b-345">remoteDependency [0] url</span></span> |<span data-ttu-id="3395b-346">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-346">string</span></span> |<span data-ttu-id="3395b-347">最大長度 2000</span><span class="sxs-lookup"><span data-stu-id="3395b-347">Max length 2000</span></span> |
| <span data-ttu-id="3395b-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="3395b-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="3395b-349">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-349">string</span></span> |<span data-ttu-id="3395b-350">最大長度 2000</span><span class="sxs-lookup"><span data-stu-id="3395b-350">Max length 2000</span></span> |
| <span data-ttu-id="3395b-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="3395b-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="3395b-352">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-352">string</span></span> | |
| <span data-ttu-id="3395b-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="3395b-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="3395b-354">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-354">string</span></span> |<span data-ttu-id="3395b-355">最大長度 200</span><span class="sxs-lookup"><span data-stu-id="3395b-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="3395b-356">要求</span><span class="sxs-lookup"><span data-stu-id="3395b-356">Requests</span></span>
<span data-ttu-id="3395b-357">由 [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest)傳送。</span><span class="sxs-lookup"><span data-stu-id="3395b-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="3395b-358">標準模組使用它回報在伺服器上測量的伺服器回應時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-358">The standard modules use this to reports server response time, measured at the server.</span></span>

| <span data-ttu-id="3395b-359">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-359">Path</span></span> | <span data-ttu-id="3395b-360">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-360">Type</span></span> | <span data-ttu-id="3395b-361">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-362">要求 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="3395b-362">request [0] count</span></span> |<span data-ttu-id="3395b-363">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-363">integer</span></span> |<span data-ttu-id="3395b-364">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="3395b-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="3395b-365">例如：4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="3395b-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="3395b-366">要求 [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="3395b-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="3395b-367">number</span><span class="sxs-lookup"><span data-stu-id="3395b-367">number</span></span> |<span data-ttu-id="3395b-368">從要求抵達到回應的時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-368">Time from request arriving to response.</span></span> <span data-ttu-id="3395b-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="3395b-369">1e7 == 1s</span></span> |
| <span data-ttu-id="3395b-370">要求 [0] id</span><span class="sxs-lookup"><span data-stu-id="3395b-370">request [0] id</span></span> |<span data-ttu-id="3395b-371">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-371">string</span></span> |<span data-ttu-id="3395b-372">作業 id</span><span class="sxs-lookup"><span data-stu-id="3395b-372">Operation id</span></span> |
| <span data-ttu-id="3395b-373">要求 [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="3395b-373">request [0] name</span></span> |<span data-ttu-id="3395b-374">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-374">string</span></span> |<span data-ttu-id="3395b-375">GET/POST + url 基底。</span><span class="sxs-lookup"><span data-stu-id="3395b-375">GET/POST + url base.</span></span>  <span data-ttu-id="3395b-376">最大長度 250</span><span class="sxs-lookup"><span data-stu-id="3395b-376">Max length 250</span></span> |
| <span data-ttu-id="3395b-377">要求 [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="3395b-377">request [0] responseCode</span></span> |<span data-ttu-id="3395b-378">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-378">integer</span></span> |<span data-ttu-id="3395b-379">傳送至用戶端的 HTTP 回應</span><span class="sxs-lookup"><span data-stu-id="3395b-379">HTTP response sent to client</span></span> |
| <span data-ttu-id="3395b-380">要求 [0] 成功</span><span class="sxs-lookup"><span data-stu-id="3395b-380">request [0] success</span></span> |<span data-ttu-id="3395b-381">布林值</span><span class="sxs-lookup"><span data-stu-id="3395b-381">boolean</span></span> |<span data-ttu-id="3395b-382">預設值 == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="3395b-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="3395b-383">要求 [0] url</span><span class="sxs-lookup"><span data-stu-id="3395b-383">request [0] url</span></span> |<span data-ttu-id="3395b-384">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-384">string</span></span> |<span data-ttu-id="3395b-385">不包括主機</span><span class="sxs-lookup"><span data-stu-id="3395b-385">Not including host</span></span> |
| <span data-ttu-id="3395b-386">要求 [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="3395b-386">request [0] urlData.base</span></span> |<span data-ttu-id="3395b-387">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-387">string</span></span> | |
| <span data-ttu-id="3395b-388">要求 [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="3395b-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="3395b-389">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-389">string</span></span> | |
| <span data-ttu-id="3395b-390">要求 [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="3395b-390">request [0] urlData.host</span></span> |<span data-ttu-id="3395b-391">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="3395b-392">頁面檢視效能</span><span class="sxs-lookup"><span data-stu-id="3395b-392">Page View Performance</span></span>
<span data-ttu-id="3395b-393">由瀏覽器傳送。</span><span class="sxs-lookup"><span data-stu-id="3395b-393">Sent by the browser.</span></span> <span data-ttu-id="3395b-394">測量處理頁面的時間，從使用者起始要求到顯示完成 (不包括非同步 AJAX 呼叫)。</span><span class="sxs-lookup"><span data-stu-id="3395b-394">Measures the time to process a page, from user initiating the request to display complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="3395b-395">內容值會顯示用戶端作業系統和瀏覽器版本。</span><span class="sxs-lookup"><span data-stu-id="3395b-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="3395b-396">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-396">Path</span></span> | <span data-ttu-id="3395b-397">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-397">Type</span></span> | <span data-ttu-id="3395b-398">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="3395b-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="3395b-400">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-400">integer</span></span> |<span data-ttu-id="3395b-401">從接收 HTML 完成到顯示頁面的時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-401">Time from end of receiving the HTML to displaying the page.</span></span> |
| <span data-ttu-id="3395b-402">clientPerformance [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="3395b-402">clientPerformance [0] name</span></span> |<span data-ttu-id="3395b-403">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-403">string</span></span> | |
| <span data-ttu-id="3395b-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="3395b-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="3395b-405">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-405">integer</span></span> |<span data-ttu-id="3395b-406">建立網路連線所需的時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-406">Time taken to establish a network connection.</span></span> |
| <span data-ttu-id="3395b-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="3395b-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="3395b-408">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-408">integer</span></span> |<span data-ttu-id="3395b-409">從傳送要求完成至接收回覆中 HTML 的時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-409">Time from end of sending the request to receiving the HTML in reply.</span></span> |
| <span data-ttu-id="3395b-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="3395b-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="3395b-411">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-411">integer</span></span> |<span data-ttu-id="3395b-412">傳送 HTTP 要求所需的時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-412">Time from taken to send the HTTP request.</span></span> |
| <span data-ttu-id="3395b-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="3395b-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="3395b-414">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-414">integer</span></span> |<span data-ttu-id="3395b-415">從開始傳送要求到顯示頁面的時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-415">Time from starting to send the request to displaying the page.</span></span> |
| <span data-ttu-id="3395b-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="3395b-416">clientPerformance [0] url</span></span> |<span data-ttu-id="3395b-417">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-417">string</span></span> |<span data-ttu-id="3395b-418">此要求的 URL</span><span class="sxs-lookup"><span data-stu-id="3395b-418">URL of this request</span></span> |
| <span data-ttu-id="3395b-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="3395b-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="3395b-420">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-420">string</span></span> | |
| <span data-ttu-id="3395b-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="3395b-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="3395b-422">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-422">string</span></span> | |
| <span data-ttu-id="3395b-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="3395b-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="3395b-424">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-424">string</span></span> | |
| <span data-ttu-id="3395b-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="3395b-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="3395b-426">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="3395b-427">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="3395b-427">Page Views</span></span>
<span data-ttu-id="3395b-428">由 trackPageView() 或 [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views) 傳送</span><span class="sxs-lookup"><span data-stu-id="3395b-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="3395b-429">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-429">Path</span></span> | <span data-ttu-id="3395b-430">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-430">Type</span></span> | <span data-ttu-id="3395b-431">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-432">檢視 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="3395b-432">view [0] count</span></span> |<span data-ttu-id="3395b-433">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-433">integer</span></span> |<span data-ttu-id="3395b-434">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="3395b-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="3395b-435">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="3395b-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="3395b-436">檢視 [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="3395b-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="3395b-437">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-437">integer</span></span> |<span data-ttu-id="3395b-438">在 trackPageView() 中或由 startTrackPage() - stopTrackPage() 選擇性設定的值。</span><span class="sxs-lookup"><span data-stu-id="3395b-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="3395b-439">和 clientPerformance 的值不同。</span><span class="sxs-lookup"><span data-stu-id="3395b-439">Not the same as clientPerformance values.</span></span> |
| <span data-ttu-id="3395b-440">檢視 [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="3395b-440">view [0] name</span></span> |<span data-ttu-id="3395b-441">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-441">string</span></span> |<span data-ttu-id="3395b-442">頁面標題。</span><span class="sxs-lookup"><span data-stu-id="3395b-442">Page title.</span></span>  <span data-ttu-id="3395b-443">最大長度 250</span><span class="sxs-lookup"><span data-stu-id="3395b-443">Max length 250</span></span> |
| <span data-ttu-id="3395b-444">檢視 [0] url</span><span class="sxs-lookup"><span data-stu-id="3395b-444">view [0] url</span></span> |<span data-ttu-id="3395b-445">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-445">string</span></span> | |
| <span data-ttu-id="3395b-446">檢視 [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="3395b-446">view [0] urlData.base</span></span> |<span data-ttu-id="3395b-447">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-447">string</span></span> | |
| <span data-ttu-id="3395b-448">檢視 [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="3395b-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="3395b-449">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-449">string</span></span> | |
| <span data-ttu-id="3395b-450">檢視 [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="3395b-450">view [0] urlData.host</span></span> |<span data-ttu-id="3395b-451">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="3395b-452">Availability</span><span class="sxs-lookup"><span data-stu-id="3395b-452">Availability</span></span>
<span data-ttu-id="3395b-453">回報 [可用性 Web 測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="3395b-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="3395b-454">Path</span><span class="sxs-lookup"><span data-stu-id="3395b-454">Path</span></span> | <span data-ttu-id="3395b-455">類型</span><span class="sxs-lookup"><span data-stu-id="3395b-455">Type</span></span> | <span data-ttu-id="3395b-456">注意事項</span><span class="sxs-lookup"><span data-stu-id="3395b-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3395b-457">可用性 [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="3395b-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="3395b-458">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-458">string</span></span> |<span data-ttu-id="3395b-459">Availability</span><span class="sxs-lookup"><span data-stu-id="3395b-459">availability</span></span> |
| <span data-ttu-id="3395b-460">可用性 [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="3395b-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="3395b-461">number</span><span class="sxs-lookup"><span data-stu-id="3395b-461">number</span></span> |<span data-ttu-id="3395b-462">1.0 或 0.0</span><span class="sxs-lookup"><span data-stu-id="3395b-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="3395b-463">可用性 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="3395b-463">availability [0] count</span></span> |<span data-ttu-id="3395b-464">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-464">integer</span></span> |<span data-ttu-id="3395b-465">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="3395b-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="3395b-466">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="3395b-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="3395b-467">可用性 [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="3395b-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="3395b-468">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-468">string</span></span> | |
| <span data-ttu-id="3395b-469">可用性 [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="3395b-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="3395b-470">integer</span><span class="sxs-lookup"><span data-stu-id="3395b-470">integer</span></span> | |
| <span data-ttu-id="3395b-471">可用性 [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="3395b-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="3395b-472">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-472">string</span></span> | |
| <span data-ttu-id="3395b-473">可用性 [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="3395b-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="3395b-474">number</span><span class="sxs-lookup"><span data-stu-id="3395b-474">number</span></span> |<span data-ttu-id="3395b-475">測試持續時間。</span><span class="sxs-lookup"><span data-stu-id="3395b-475">Duration of test.</span></span> <span data-ttu-id="3395b-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="3395b-476">1e7==1s</span></span> |
| <span data-ttu-id="3395b-477">可用性 [0] 訊息</span><span class="sxs-lookup"><span data-stu-id="3395b-477">availability [0] message</span></span> |<span data-ttu-id="3395b-478">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-478">string</span></span> |<span data-ttu-id="3395b-479">失敗診斷</span><span class="sxs-lookup"><span data-stu-id="3395b-479">Failure diagnostic</span></span> |
| <span data-ttu-id="3395b-480">可用性 [0] 結果</span><span class="sxs-lookup"><span data-stu-id="3395b-480">availability [0] result</span></span> |<span data-ttu-id="3395b-481">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-481">string</span></span> |<span data-ttu-id="3395b-482">通過/失敗</span><span class="sxs-lookup"><span data-stu-id="3395b-482">Pass/Fail</span></span> |
| <span data-ttu-id="3395b-483">可用性 [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="3395b-483">availability [0] runLocation</span></span> |<span data-ttu-id="3395b-484">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-484">string</span></span> |<span data-ttu-id="3395b-485">http req 的地理區域來源</span><span class="sxs-lookup"><span data-stu-id="3395b-485">Geo source of http req</span></span> |
| <span data-ttu-id="3395b-486">可用性 [0] testName</span><span class="sxs-lookup"><span data-stu-id="3395b-486">availability [0] testName</span></span> |<span data-ttu-id="3395b-487">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-487">string</span></span> | |
| <span data-ttu-id="3395b-488">可用性 [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="3395b-488">availability [0] testRunId</span></span> |<span data-ttu-id="3395b-489">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-489">string</span></span> | |
| <span data-ttu-id="3395b-490">可用性 [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="3395b-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="3395b-491">字串</span><span class="sxs-lookup"><span data-stu-id="3395b-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="3395b-492">度量</span><span class="sxs-lookup"><span data-stu-id="3395b-492">Metrics</span></span>
<span data-ttu-id="3395b-493">由 TrackMetric() 產生。</span><span class="sxs-lookup"><span data-stu-id="3395b-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="3395b-494">度量值位於 context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="3395b-494">The metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="3395b-495">例如：</span><span class="sxs-lookup"><span data-stu-id="3395b-495">For example:</span></span>

    {
     "metric": [ ],
     "context": {
     ...
     "custom": {
        "dimensions": [
          { "ProcessId": "4068" }
        ],
        "metrics": [
          {
            "dispatchRate": {
              "value": 0.001295,
              "count": 1.0,
              "min": 0.001295,
              "max": 0.001295,
              "stdDev": 0.0,
              "sampledValue": 0.001295,
              "sum": 0.001295
            }
          }
         } ] }
    }

## <a name="about-metric-values"></a><span data-ttu-id="3395b-496">關於度量值</span><span class="sxs-lookup"><span data-stu-id="3395b-496">About metric values</span></span>
<span data-ttu-id="3395b-497">在度量報告和其他位置中的度量值，會利用標準物件結構回報。</span><span class="sxs-lookup"><span data-stu-id="3395b-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="3395b-498">例如：</span><span class="sxs-lookup"><span data-stu-id="3395b-498">For example:</span></span>

      "durationMetric": {
        "name": "contoso.org",
        "type": "Aggregation",
        "value": 468.71603053650279,
        "count": 1.0,
        "min": 468.71603053650279,
        "max": 468.71603053650279,
        "stdDev": 0.0,
        "sampledValue": 468.71603053650279
      }

<span data-ttu-id="3395b-499">目前 - 不過未來可能會變更 - 在所有從標準 SDK 模組回報的值中，`count==1` 以及只有 `name` 和 `value` 欄位是有用的。</span><span class="sxs-lookup"><span data-stu-id="3395b-499">Currently - though this might change in the future - in all values reported from the standard SDK modules, `count==1` and only the `name` and `value` fields are useful.</span></span> <span data-ttu-id="3395b-500">它們會有差異的唯一案例是，如果您撰寫自己的 TrackMetric 呼叫，而且您在其中設定其他參數。</span><span class="sxs-lookup"><span data-stu-id="3395b-500">The only case where they would be different would be if you write your own TrackMetric calls in which you set the other parameters.</span></span>

<span data-ttu-id="3395b-501">其他欄位的目的是允許度量在 SDK 中彙總，以減少入口網站的流量。</span><span class="sxs-lookup"><span data-stu-id="3395b-501">The purpose of the other fields is to allow metrics to be aggregated in the SDK, to reduce traffic to the portal.</span></span> <span data-ttu-id="3395b-502">例如，您可以在傳送每個度量報告之前平均數個連續的讀數。</span><span class="sxs-lookup"><span data-stu-id="3395b-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="3395b-503">然後您會計算 min、max、標準差和彙總值 (sum 或 average)，並將計數設為報告所代表的讀數數目。</span><span class="sxs-lookup"><span data-stu-id="3395b-503">Then you would calculate the min, max, standard deviation and aggregate value (sum or average) and set count to the number of readings represented by the report.</span></span>

<span data-ttu-id="3395b-504">在上述資料表中，我們省略了很少使用的欄位計數、min、max、stdDev 和 sampledValue。</span><span class="sxs-lookup"><span data-stu-id="3395b-504">In the tables above, we have omitted the rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="3395b-505">除了使用預先彙總的度量，如果您需要減少遙測量，您可以改為使用 [取樣](app-insights-sampling.md) 。</span><span class="sxs-lookup"><span data-stu-id="3395b-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need to reduce the volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="3395b-506">持續時間</span><span class="sxs-lookup"><span data-stu-id="3395b-506">Durations</span></span>
<span data-ttu-id="3395b-507">除非另有說明，否則持續時間皆以十分之一微秒表示，所以 10000000.0 表示 1 秒。</span><span class="sxs-lookup"><span data-stu-id="3395b-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="3395b-508">另請參閱</span><span class="sxs-lookup"><span data-stu-id="3395b-508">See also</span></span>
* [<span data-ttu-id="3395b-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="3395b-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="3395b-510">連續匯出</span><span class="sxs-lookup"><span data-stu-id="3395b-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="3395b-511">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="3395b-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
