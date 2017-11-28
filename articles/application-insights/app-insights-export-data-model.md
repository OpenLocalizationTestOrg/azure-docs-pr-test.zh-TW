---
title: "aaaAzure 應用程式的 Insights 資料模型 |Microsoft 文件"
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
ms.openlocfilehash: 5ff3ce7953b91cc69b5d96c0ea9b6d58a6016e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-export-data-model"></a><span data-ttu-id="d1406-103">Application Insights 匯出資料模型</span><span class="sxs-lookup"><span data-stu-id="d1406-103">Application Insights Export Data Model</span></span>
<span data-ttu-id="d1406-104">下表列出的遙測資料從 hello 傳送 hello 屬性[Application Insights](app-insights-overview.md) Sdk toohello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d1406-104">This table lists hello properties of telemetry sent from hello [Application Insights](app-insights-overview.md) SDKs toohello portal.</span></span>
<span data-ttu-id="d1406-105">您會在 [連續匯出](app-insights-export-telemetry.md)的資料輸出中看到這些屬性。</span><span class="sxs-lookup"><span data-stu-id="d1406-105">You'll see these properties in data output from [Continuous Export](app-insights-export-telemetry.md).</span></span>
<span data-ttu-id="d1406-106">它們也會出現在[計量瀏覽器](app-insights-metrics-explorer.md)和[診斷搜尋](app-insights-diagnostic-search.md)的屬性篩選中。</span><span class="sxs-lookup"><span data-stu-id="d1406-106">They also appear in property filters in [Metric Explorer](app-insights-metrics-explorer.md) and [Diagnostic Search](app-insights-diagnostic-search.md).</span></span>

<span data-ttu-id="d1406-107">點 toonote:</span><span class="sxs-lookup"><span data-stu-id="d1406-107">Points toonote:</span></span>

* <span data-ttu-id="d1406-108">`[0]`這些資料表中代表 hello 您擁有其路徑 tooinsert 索引; 中的點但它不一定是 0。</span><span class="sxs-lookup"><span data-stu-id="d1406-108">`[0]` in these tables denotes a point in hello path where you have tooinsert an index; but it isn't always 0.</span></span>
* <span data-ttu-id="d1406-109">持續時間的長度單位是微秒，因此 10000000 == 1 秒。</span><span class="sxs-lookup"><span data-stu-id="d1406-109">Time durations are in tenths of a microsecond, so 10000000 == 1 second.</span></span>
* <span data-ttu-id="d1406-110">日期和時間是 UTC，並可以在 hello ISO 格式`yyyy-MM-DDThh:mm:ss.sssZ`</span><span class="sxs-lookup"><span data-stu-id="d1406-110">Dates and times are UTC, and are given in hello ISO format `yyyy-MM-DDThh:mm:ss.sssZ`</span></span>


## <a name="example"></a><span data-ttu-id="d1406-111">範例</span><span class="sxs-lookup"><span data-stu-id="d1406-111">Example</span></span>
    // A server report about an HTTP request
    {
    "request": [
      {
        "urlData": { // derived from 'url'
          "host": "contoso.org",
          "base": "/",
          "hashTag": ""
        },
        "responseCode": 200, // Sent tooclient
        "success": true, // Default == responseCode<400
        // Request id becomes hello operation id of child events
        "id": "fCOhCdCnZ9I=",  
        "name": "GET Home/Index",
        "count": 1, // 100% / sampling rate
        "durationMetric": {
          "value": 1046804.0, // 10000000 == 1 second
          // Currently hello following fields are redundant:
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
        // last octagon is anonymized too0 at portal:
        "clientip": "168.62.177.0",
        "province": "",
        "city": ""
      },
      "data": {
        "isSynthetic": true, // we identified source as a bot
        // percentage of generated data sent tooportal:
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
  <span data-ttu-id="d1406-112">}</span><span class="sxs-lookup"><span data-stu-id="d1406-112">}</span></span>

## <a name="context"></a><span data-ttu-id="d1406-113">Context</span><span class="sxs-lookup"><span data-stu-id="d1406-113">Context</span></span>
<span data-ttu-id="d1406-114">所有類型的遙測都會伴隨內容區段。</span><span class="sxs-lookup"><span data-stu-id="d1406-114">All types of telemetry are accompanied by a context section.</span></span> <span data-ttu-id="d1406-115">並非所有的欄位都會連同每個資料點傳輸。</span><span class="sxs-lookup"><span data-stu-id="d1406-115">Not all of these fields are transmitted with every data point.</span></span>

| <span data-ttu-id="d1406-116">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-116">Path</span></span> | <span data-ttu-id="d1406-117">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-117">Type</span></span> | <span data-ttu-id="d1406-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-118">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-119">context.custom.dimensions [0]</span><span class="sxs-lookup"><span data-stu-id="d1406-119">context.custom.dimensions [0]</span></span> |<span data-ttu-id="d1406-120">物件 [ ]</span><span class="sxs-lookup"><span data-stu-id="d1406-120">object [ ]</span></span> |<span data-ttu-id="d1406-121">由自訂屬性參數設定的索引鍵-值字串組。</span><span class="sxs-lookup"><span data-stu-id="d1406-121">Key-value string pairs set by custom properties parameter.</span></span> <span data-ttu-id="d1406-122">索引鍵的最大長度 100，值的最大長度 1024。</span><span class="sxs-lookup"><span data-stu-id="d1406-122">Key max length 100, values max length 1024.</span></span> <span data-ttu-id="d1406-123">超過 100 個唯一值的 hello 屬性可搜尋，但不能用於分割。</span><span class="sxs-lookup"><span data-stu-id="d1406-123">More than 100 unique values, hello property can be searched but cannot be used for segmentation.</span></span> <span data-ttu-id="d1406-124">每個 ikey 的最大值 200 索引鍵。</span><span class="sxs-lookup"><span data-stu-id="d1406-124">Max 200 keys per ikey.</span></span> |
| <span data-ttu-id="d1406-125">context.custom.metrics [0]</span><span class="sxs-lookup"><span data-stu-id="d1406-125">context.custom.metrics [0]</span></span> |<span data-ttu-id="d1406-126">物件 [ ]</span><span class="sxs-lookup"><span data-stu-id="d1406-126">object [ ]</span></span> |<span data-ttu-id="d1406-127">由自訂測量參數和 TrackMetrics 設定的索引鍵-值組。</span><span class="sxs-lookup"><span data-stu-id="d1406-127">Key-value pairs set by custom measurements parameter and by TrackMetrics.</span></span> <span data-ttu-id="d1406-128">索引鍵的最大長度 100，值可能為數值。</span><span class="sxs-lookup"><span data-stu-id="d1406-128">Key max length 100, values may be numeric.</span></span> |
| <span data-ttu-id="d1406-129">context.data.eventTime</span><span class="sxs-lookup"><span data-stu-id="d1406-129">context.data.eventTime</span></span> |<span data-ttu-id="d1406-130">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-130">string</span></span> |<span data-ttu-id="d1406-131">UTC</span><span class="sxs-lookup"><span data-stu-id="d1406-131">UTC</span></span> |
| <span data-ttu-id="d1406-132">context.data.isSynthetic</span><span class="sxs-lookup"><span data-stu-id="d1406-132">context.data.isSynthetic</span></span> |<span data-ttu-id="d1406-133">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-133">boolean</span></span> |<span data-ttu-id="d1406-134">要求出現 toocome 從 bot 或 web 測試。</span><span class="sxs-lookup"><span data-stu-id="d1406-134">Request appears toocome from a bot or web test.</span></span> |
| <span data-ttu-id="d1406-135">context.data.samplingRate</span><span class="sxs-lookup"><span data-stu-id="d1406-135">context.data.samplingRate</span></span> |<span data-ttu-id="d1406-136">number</span><span class="sxs-lookup"><span data-stu-id="d1406-136">number</span></span> |<span data-ttu-id="d1406-137">Hello 傳送 tooportal SDK 所產生的遙測的百分比。</span><span class="sxs-lookup"><span data-stu-id="d1406-137">Percentage of telemetry generated by hello SDK that is sent tooportal.</span></span> <span data-ttu-id="d1406-138">範圍 0.0-100.0。</span><span class="sxs-lookup"><span data-stu-id="d1406-138">Range 0.0-100.0.</span></span> |
| <span data-ttu-id="d1406-139">context.device</span><span class="sxs-lookup"><span data-stu-id="d1406-139">context.device</span></span> |<span data-ttu-id="d1406-140">物件</span><span class="sxs-lookup"><span data-stu-id="d1406-140">object</span></span> |<span data-ttu-id="d1406-141">用戶端裝置</span><span class="sxs-lookup"><span data-stu-id="d1406-141">Client device</span></span> |
| <span data-ttu-id="d1406-142">context.device.browser</span><span class="sxs-lookup"><span data-stu-id="d1406-142">context.device.browser</span></span> |<span data-ttu-id="d1406-143">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-143">string</span></span> |<span data-ttu-id="d1406-144">IE, Chrome, ...</span><span class="sxs-lookup"><span data-stu-id="d1406-144">IE, Chrome, ...</span></span> |
| <span data-ttu-id="d1406-145">context.device.browserVersion</span><span class="sxs-lookup"><span data-stu-id="d1406-145">context.device.browserVersion</span></span> |<span data-ttu-id="d1406-146">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-146">string</span></span> |<span data-ttu-id="d1406-147">Chrome 48.0, ...</span><span class="sxs-lookup"><span data-stu-id="d1406-147">Chrome 48.0, ...</span></span> |
| <span data-ttu-id="d1406-148">context.device.deviceModel</span><span class="sxs-lookup"><span data-stu-id="d1406-148">context.device.deviceModel</span></span> |<span data-ttu-id="d1406-149">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-149">string</span></span> | |
| <span data-ttu-id="d1406-150">context.device.deviceName</span><span class="sxs-lookup"><span data-stu-id="d1406-150">context.device.deviceName</span></span> |<span data-ttu-id="d1406-151">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-151">string</span></span> | |
| <span data-ttu-id="d1406-152">context.device.id</span><span class="sxs-lookup"><span data-stu-id="d1406-152">context.device.id</span></span> |<span data-ttu-id="d1406-153">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-153">string</span></span> | |
| <span data-ttu-id="d1406-154">context.device.locale</span><span class="sxs-lookup"><span data-stu-id="d1406-154">context.device.locale</span></span> |<span data-ttu-id="d1406-155">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-155">string</span></span> |<span data-ttu-id="d1406-156">en-GB, de-DE, ...</span><span class="sxs-lookup"><span data-stu-id="d1406-156">en-GB, de-DE, ...</span></span> |
| <span data-ttu-id="d1406-157">context.device.network</span><span class="sxs-lookup"><span data-stu-id="d1406-157">context.device.network</span></span> |<span data-ttu-id="d1406-158">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-158">string</span></span> | |
| <span data-ttu-id="d1406-159">context.device.oemName</span><span class="sxs-lookup"><span data-stu-id="d1406-159">context.device.oemName</span></span> |<span data-ttu-id="d1406-160">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-160">string</span></span> | |
| <span data-ttu-id="d1406-161">context.device.osVersion</span><span class="sxs-lookup"><span data-stu-id="d1406-161">context.device.osVersion</span></span> |<span data-ttu-id="d1406-162">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-162">string</span></span> |<span data-ttu-id="d1406-163">主機作業系統</span><span class="sxs-lookup"><span data-stu-id="d1406-163">Host OS</span></span> |
| <span data-ttu-id="d1406-164">context.device.roleInstance</span><span class="sxs-lookup"><span data-stu-id="d1406-164">context.device.roleInstance</span></span> |<span data-ttu-id="d1406-165">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-165">string</span></span> |<span data-ttu-id="d1406-166">伺服器主機的識別碼</span><span class="sxs-lookup"><span data-stu-id="d1406-166">ID of server host</span></span> |
| <span data-ttu-id="d1406-167">context.device.roleName</span><span class="sxs-lookup"><span data-stu-id="d1406-167">context.device.roleName</span></span> |<span data-ttu-id="d1406-168">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-168">string</span></span> | |
| <span data-ttu-id="d1406-169">context.device.type</span><span class="sxs-lookup"><span data-stu-id="d1406-169">context.device.type</span></span> |<span data-ttu-id="d1406-170">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-170">string</span></span> |<span data-ttu-id="d1406-171">PC, Browser, ...</span><span class="sxs-lookup"><span data-stu-id="d1406-171">PC, Browser, ...</span></span> |
| <span data-ttu-id="d1406-172">context.location</span><span class="sxs-lookup"><span data-stu-id="d1406-172">context.location</span></span> |<span data-ttu-id="d1406-173">物件</span><span class="sxs-lookup"><span data-stu-id="d1406-173">object</span></span> |<span data-ttu-id="d1406-174">衍生自 clientip。</span><span class="sxs-lookup"><span data-stu-id="d1406-174">Derived from clientip.</span></span> |
| <span data-ttu-id="d1406-175">context.location.city</span><span class="sxs-lookup"><span data-stu-id="d1406-175">context.location.city</span></span> |<span data-ttu-id="d1406-176">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-176">string</span></span> |<span data-ttu-id="d1406-177">衍生自 clientip (如果已知)</span><span class="sxs-lookup"><span data-stu-id="d1406-177">Derived from clientip, if known</span></span> |
| <span data-ttu-id="d1406-178">context.location.clientip</span><span class="sxs-lookup"><span data-stu-id="d1406-178">context.location.clientip</span></span> |<span data-ttu-id="d1406-179">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-179">string</span></span> |<span data-ttu-id="d1406-180">最後一個八邊形是匿名的 too0。</span><span class="sxs-lookup"><span data-stu-id="d1406-180">Last octagon is anonymized too0.</span></span> |
| <span data-ttu-id="d1406-181">context.location.continent</span><span class="sxs-lookup"><span data-stu-id="d1406-181">context.location.continent</span></span> |<span data-ttu-id="d1406-182">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-182">string</span></span> | |
| <span data-ttu-id="d1406-183">context.location.country</span><span class="sxs-lookup"><span data-stu-id="d1406-183">context.location.country</span></span> |<span data-ttu-id="d1406-184">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-184">string</span></span> | |
| <span data-ttu-id="d1406-185">context.location.province</span><span class="sxs-lookup"><span data-stu-id="d1406-185">context.location.province</span></span> |<span data-ttu-id="d1406-186">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-186">string</span></span> |<span data-ttu-id="d1406-187">州或省</span><span class="sxs-lookup"><span data-stu-id="d1406-187">State or province</span></span> |
| <span data-ttu-id="d1406-188">context.operation.id</span><span class="sxs-lookup"><span data-stu-id="d1406-188">context.operation.id</span></span> |<span data-ttu-id="d1406-189">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-189">string</span></span> |<span data-ttu-id="d1406-190">具有相同的作業識別碼時，會顯示為相關項目上，在 hello 入口網站中的 hello 的項目。</span><span class="sxs-lookup"><span data-stu-id="d1406-190">Items that have hello same operation id are shown as Related Items in hello portal.</span></span> <span data-ttu-id="d1406-191">通常 hello 要求識別碼。</span><span class="sxs-lookup"><span data-stu-id="d1406-191">Usually hello request id.</span></span> |
| <span data-ttu-id="d1406-192">context.operation.name</span><span class="sxs-lookup"><span data-stu-id="d1406-192">context.operation.name</span></span> |<span data-ttu-id="d1406-193">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-193">string</span></span> |<span data-ttu-id="d1406-194">url 或要求名稱</span><span class="sxs-lookup"><span data-stu-id="d1406-194">url or request name</span></span> |
| <span data-ttu-id="d1406-195">context.operation.parentId</span><span class="sxs-lookup"><span data-stu-id="d1406-195">context.operation.parentId</span></span> |<span data-ttu-id="d1406-196">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-196">string</span></span> |<span data-ttu-id="d1406-197">允許巢狀的相關項目。</span><span class="sxs-lookup"><span data-stu-id="d1406-197">Allows nested related items.</span></span> |
| <span data-ttu-id="d1406-198">context.session.id</span><span class="sxs-lookup"><span data-stu-id="d1406-198">context.session.id</span></span> |<span data-ttu-id="d1406-199">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-199">string</span></span> |<span data-ttu-id="d1406-200">Hello 中的作業群組的識別碼相同的來源。</span><span class="sxs-lookup"><span data-stu-id="d1406-200">Id of a group of operations from hello same source.</span></span> <span data-ttu-id="d1406-201">不執行動作的 30 分鐘的期間發出訊號 hello 工作階段結束。</span><span class="sxs-lookup"><span data-stu-id="d1406-201">A period of 30 minutes without an operation signals hello end of a session.</span></span> |
| <span data-ttu-id="d1406-202">context.session.isFirst</span><span class="sxs-lookup"><span data-stu-id="d1406-202">context.session.isFirst</span></span> |<span data-ttu-id="d1406-203">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-203">boolean</span></span> | |
| <span data-ttu-id="d1406-204">context.user.accountAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="d1406-204">context.user.accountAcquisitionDate</span></span> |<span data-ttu-id="d1406-205">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-205">string</span></span> | |
| <span data-ttu-id="d1406-206">context.user.anonAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="d1406-206">context.user.anonAcquisitionDate</span></span> |<span data-ttu-id="d1406-207">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-207">string</span></span> | |
| <span data-ttu-id="d1406-208">context.user.anonId</span><span class="sxs-lookup"><span data-stu-id="d1406-208">context.user.anonId</span></span> |<span data-ttu-id="d1406-209">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-209">string</span></span> | |
| <span data-ttu-id="d1406-210">context.user.authAcquisitionDate</span><span class="sxs-lookup"><span data-stu-id="d1406-210">context.user.authAcquisitionDate</span></span> |<span data-ttu-id="d1406-211">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-211">string</span></span> |[<span data-ttu-id="d1406-212">已驗證的使用者</span><span class="sxs-lookup"><span data-stu-id="d1406-212">Authenticated User</span></span>](app-insights-api-custom-events-metrics.md#authenticated-users) |
| <span data-ttu-id="d1406-213">context.user.isAuthenticated</span><span class="sxs-lookup"><span data-stu-id="d1406-213">context.user.isAuthenticated</span></span> |<span data-ttu-id="d1406-214">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-214">boolean</span></span> | |
| <span data-ttu-id="d1406-215">internal.data.documentVersion</span><span class="sxs-lookup"><span data-stu-id="d1406-215">internal.data.documentVersion</span></span> |<span data-ttu-id="d1406-216">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-216">string</span></span> | |
| <span data-ttu-id="d1406-217">internal.data.id</span><span class="sxs-lookup"><span data-stu-id="d1406-217">internal.data.id</span></span> |<span data-ttu-id="d1406-218">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-218">string</span></span> | |

## <a name="events"></a><span data-ttu-id="d1406-219">事件</span><span class="sxs-lookup"><span data-stu-id="d1406-219">Events</span></span>
<span data-ttu-id="d1406-220">[TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent)產生的自訂事件。</span><span class="sxs-lookup"><span data-stu-id="d1406-220">Custom events generated by [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

| <span data-ttu-id="d1406-221">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-221">Path</span></span> | <span data-ttu-id="d1406-222">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-222">Type</span></span> | <span data-ttu-id="d1406-223">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-223">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-224">事件 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="d1406-224">event [0] count</span></span> |<span data-ttu-id="d1406-225">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-225">integer</span></span> |<span data-ttu-id="d1406-226">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="d1406-226">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="d1406-227">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="d1406-227">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="d1406-228">事件 [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="d1406-228">event [0] name</span></span> |<span data-ttu-id="d1406-229">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-229">string</span></span> |<span data-ttu-id="d1406-230">事件名稱。</span><span class="sxs-lookup"><span data-stu-id="d1406-230">Event name.</span></span>  <span data-ttu-id="d1406-231">最大長度 250。</span><span class="sxs-lookup"><span data-stu-id="d1406-231">Max length 250.</span></span> |
| <span data-ttu-id="d1406-232">事件 [0] url</span><span class="sxs-lookup"><span data-stu-id="d1406-232">event [0] url</span></span> |<span data-ttu-id="d1406-233">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-233">string</span></span> | |
| <span data-ttu-id="d1406-234">事件 [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="d1406-234">event [0] urlData.base</span></span> |<span data-ttu-id="d1406-235">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-235">string</span></span> | |
| <span data-ttu-id="d1406-236">事件 [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="d1406-236">event [0] urlData.host</span></span> |<span data-ttu-id="d1406-237">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-237">string</span></span> | |

## <a name="exceptions"></a><span data-ttu-id="d1406-238">例外狀況</span><span class="sxs-lookup"><span data-stu-id="d1406-238">Exceptions</span></span>
<span data-ttu-id="d1406-239">報表[例外狀況](app-insights-asp-net-exceptions.md)hello 瀏覽器和伺服器 hello 中。</span><span class="sxs-lookup"><span data-stu-id="d1406-239">Reports [exceptions](app-insights-asp-net-exceptions.md) in hello server and in hello browser.</span></span>

| <span data-ttu-id="d1406-240">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-240">Path</span></span> | <span data-ttu-id="d1406-241">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-241">Type</span></span> | <span data-ttu-id="d1406-242">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-242">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-243">basicException [0] 組件</span><span class="sxs-lookup"><span data-stu-id="d1406-243">basicException [0] assembly</span></span> |<span data-ttu-id="d1406-244">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-244">string</span></span> | |
| <span data-ttu-id="d1406-245">basicException [0] 計數</span><span class="sxs-lookup"><span data-stu-id="d1406-245">basicException [0] count</span></span> |<span data-ttu-id="d1406-246">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-246">integer</span></span> |<span data-ttu-id="d1406-247">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="d1406-247">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="d1406-248">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="d1406-248">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="d1406-249">basicException [0] exceptionGroup</span><span class="sxs-lookup"><span data-stu-id="d1406-249">basicException [0] exceptionGroup</span></span> |<span data-ttu-id="d1406-250">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-250">string</span></span> | |
| <span data-ttu-id="d1406-251">basicException [0] exceptionType</span><span class="sxs-lookup"><span data-stu-id="d1406-251">basicException [0] exceptionType</span></span> |<span data-ttu-id="d1406-252">string</span><span class="sxs-lookup"><span data-stu-id="d1406-252">string</span></span> | |
| <span data-ttu-id="d1406-253">basicException [0] failedUserCodeMethod</span><span class="sxs-lookup"><span data-stu-id="d1406-253">basicException [0] failedUserCodeMethod</span></span> |<span data-ttu-id="d1406-254">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-254">string</span></span> | |
| <span data-ttu-id="d1406-255">basicException [0] failedUserCodeAssembly</span><span class="sxs-lookup"><span data-stu-id="d1406-255">basicException [0] failedUserCodeAssembly</span></span> |<span data-ttu-id="d1406-256">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-256">string</span></span> | |
| <span data-ttu-id="d1406-257">basicException [0] handledAt</span><span class="sxs-lookup"><span data-stu-id="d1406-257">basicException [0] handledAt</span></span> |<span data-ttu-id="d1406-258">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-258">string</span></span> | |
| <span data-ttu-id="d1406-259">basicException [0] hasFullStack</span><span class="sxs-lookup"><span data-stu-id="d1406-259">basicException [0] hasFullStack</span></span> |<span data-ttu-id="d1406-260">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-260">boolean</span></span> | |
| <span data-ttu-id="d1406-261">basicException [0] id</span><span class="sxs-lookup"><span data-stu-id="d1406-261">basicException [0] id</span></span> |<span data-ttu-id="d1406-262">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-262">string</span></span> | |
| <span data-ttu-id="d1406-263">basicException [0] 方法</span><span class="sxs-lookup"><span data-stu-id="d1406-263">basicException [0] method</span></span> |<span data-ttu-id="d1406-264">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-264">string</span></span> | |
| <span data-ttu-id="d1406-265">basicException [0] 訊息</span><span class="sxs-lookup"><span data-stu-id="d1406-265">basicException [0] message</span></span> |<span data-ttu-id="d1406-266">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-266">string</span></span> |<span data-ttu-id="d1406-267">例外狀況訊息。</span><span class="sxs-lookup"><span data-stu-id="d1406-267">Exception message.</span></span> <span data-ttu-id="d1406-268">最大長度 10k。</span><span class="sxs-lookup"><span data-stu-id="d1406-268">Max length 10k.</span></span> |
| <span data-ttu-id="d1406-269">basicException [0] outerExceptionMessage</span><span class="sxs-lookup"><span data-stu-id="d1406-269">basicException [0] outerExceptionMessage</span></span> |<span data-ttu-id="d1406-270">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-270">string</span></span> | |
| <span data-ttu-id="d1406-271">basicException [0] outerExceptionThrownAtAssembly</span><span class="sxs-lookup"><span data-stu-id="d1406-271">basicException [0] outerExceptionThrownAtAssembly</span></span> |<span data-ttu-id="d1406-272">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-272">string</span></span> | |
| <span data-ttu-id="d1406-273">basicException [0] outerExceptionThrownAtMethod</span><span class="sxs-lookup"><span data-stu-id="d1406-273">basicException [0] outerExceptionThrownAtMethod</span></span> |<span data-ttu-id="d1406-274">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-274">string</span></span> | |
| <span data-ttu-id="d1406-275">basicException [0] outerExceptionType</span><span class="sxs-lookup"><span data-stu-id="d1406-275">basicException [0] outerExceptionType</span></span> |<span data-ttu-id="d1406-276">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-276">string</span></span> | |
| <span data-ttu-id="d1406-277">basicException [0] outerId</span><span class="sxs-lookup"><span data-stu-id="d1406-277">basicException [0] outerId</span></span> |<span data-ttu-id="d1406-278">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-278">string</span></span> | |
| <span data-ttu-id="d1406-279">basicException [0] parsedStack [0] 組件</span><span class="sxs-lookup"><span data-stu-id="d1406-279">basicException [0] parsedStack [0] assembly</span></span> |<span data-ttu-id="d1406-280">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-280">string</span></span> | |
| <span data-ttu-id="d1406-281">basicException [0] parsedStack [0] fileName</span><span class="sxs-lookup"><span data-stu-id="d1406-281">basicException [0] parsedStack [0] fileName</span></span> |<span data-ttu-id="d1406-282">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-282">string</span></span> | |
| <span data-ttu-id="d1406-283">basicException [0] parsedStack [0] 層級</span><span class="sxs-lookup"><span data-stu-id="d1406-283">basicException [0] parsedStack [0] level</span></span> |<span data-ttu-id="d1406-284">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-284">integer</span></span> | |
| <span data-ttu-id="d1406-285">basicException [0] parsedStack [0] 列</span><span class="sxs-lookup"><span data-stu-id="d1406-285">basicException [0] parsedStack [0] line</span></span> |<span data-ttu-id="d1406-286">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-286">integer</span></span> | |
| <span data-ttu-id="d1406-287">basicException [0] parsedStack [0] 方法</span><span class="sxs-lookup"><span data-stu-id="d1406-287">basicException [0] parsedStack [0] method</span></span> |<span data-ttu-id="d1406-288">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-288">string</span></span> | |
| <span data-ttu-id="d1406-289">basicException [0] 堆疊</span><span class="sxs-lookup"><span data-stu-id="d1406-289">basicException [0] stack</span></span> |<span data-ttu-id="d1406-290">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-290">string</span></span> |<span data-ttu-id="d1406-291">最大長度 10k</span><span class="sxs-lookup"><span data-stu-id="d1406-291">Max length 10k</span></span> |
| <span data-ttu-id="d1406-292">basicException [0] typeName</span><span class="sxs-lookup"><span data-stu-id="d1406-292">basicException [0] typeName</span></span> |<span data-ttu-id="d1406-293">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-293">string</span></span> | |

## <a name="trace-messages"></a><span data-ttu-id="d1406-294">追蹤訊息</span><span class="sxs-lookup"><span data-stu-id="d1406-294">Trace Messages</span></span>
<span data-ttu-id="d1406-295">由傳送[TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace)，以及 hello[記錄配接器](app-insights-asp-net-trace-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="d1406-295">Sent by [TrackTrace](app-insights-api-custom-events-metrics.md#tracktrace), and by hello [logging adapters](app-insights-asp-net-trace-logs.md).</span></span>

| <span data-ttu-id="d1406-296">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-296">Path</span></span> | <span data-ttu-id="d1406-297">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-297">Type</span></span> | <span data-ttu-id="d1406-298">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-298">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-299">訊息 [0] loggerName</span><span class="sxs-lookup"><span data-stu-id="d1406-299">message [0] loggerName</span></span> |<span data-ttu-id="d1406-300">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-300">string</span></span> | |
| <span data-ttu-id="d1406-301">訊息 [0] 參數</span><span class="sxs-lookup"><span data-stu-id="d1406-301">message [0] parameters</span></span> |<span data-ttu-id="d1406-302">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-302">string</span></span> | |
| <span data-ttu-id="d1406-303">訊息 [0] 原始碼</span><span class="sxs-lookup"><span data-stu-id="d1406-303">message [0] raw</span></span> |<span data-ttu-id="d1406-304">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-304">string</span></span> |<span data-ttu-id="d1406-305">最大長度 10 k hello 記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="d1406-305">hello log message, max length 10k.</span></span> |
| <span data-ttu-id="d1406-306">訊息 [0] severityLevel</span><span class="sxs-lookup"><span data-stu-id="d1406-306">message [0] severityLevel</span></span> |<span data-ttu-id="d1406-307">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-307">string</span></span> | |

## <a name="remote-dependency"></a><span data-ttu-id="d1406-308">遠端相依性</span><span class="sxs-lookup"><span data-stu-id="d1406-308">Remote dependency</span></span>
<span data-ttu-id="d1406-309">由 TrackDependency 傳送。</span><span class="sxs-lookup"><span data-stu-id="d1406-309">Sent by TrackDependency.</span></span> <span data-ttu-id="d1406-310">使用 tooreport 效能和使用方式[呼叫 toodependencies](app-insights-asp-net-dependencies.md) hello 伺服器和 hello 瀏覽器中的 AJAX 呼叫中。</span><span class="sxs-lookup"><span data-stu-id="d1406-310">Used tooreport performance and usage of [calls toodependencies](app-insights-asp-net-dependencies.md) in hello server, and AJAX calls in hello browser.</span></span>

| <span data-ttu-id="d1406-311">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-311">Path</span></span> | <span data-ttu-id="d1406-312">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-312">Type</span></span> | <span data-ttu-id="d1406-313">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-313">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-314">remoteDependency [0] async</span><span class="sxs-lookup"><span data-stu-id="d1406-314">remoteDependency [0] async</span></span> |<span data-ttu-id="d1406-315">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-315">boolean</span></span> | |
| <span data-ttu-id="d1406-316">remoteDependency [0] baseName</span><span class="sxs-lookup"><span data-stu-id="d1406-316">remoteDependency [0] baseName</span></span> |<span data-ttu-id="d1406-317">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-317">string</span></span> | |
| <span data-ttu-id="d1406-318">remoteDependency [0] commandName</span><span class="sxs-lookup"><span data-stu-id="d1406-318">remoteDependency [0] commandName</span></span> |<span data-ttu-id="d1406-319">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-319">string</span></span> |<span data-ttu-id="d1406-320">例如 "home/index"</span><span class="sxs-lookup"><span data-stu-id="d1406-320">For example "home/index"</span></span> |
| <span data-ttu-id="d1406-321">remoteDependency [0] 計數</span><span class="sxs-lookup"><span data-stu-id="d1406-321">remoteDependency [0] count</span></span> |<span data-ttu-id="d1406-322">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-322">integer</span></span> |<span data-ttu-id="d1406-323">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="d1406-323">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="d1406-324">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="d1406-324">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="d1406-325">remoteDependency [0] dependencyTypeName</span><span class="sxs-lookup"><span data-stu-id="d1406-325">remoteDependency [0] dependencyTypeName</span></span> |<span data-ttu-id="d1406-326">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-326">string</span></span> |<span data-ttu-id="d1406-327">HTTP、SQL、...</span><span class="sxs-lookup"><span data-stu-id="d1406-327">HTTP, SQL, ...</span></span> |
| <span data-ttu-id="d1406-328">remoteDependency [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="d1406-328">remoteDependency [0] durationMetric.value</span></span> |<span data-ttu-id="d1406-329">number</span><span class="sxs-lookup"><span data-stu-id="d1406-329">number</span></span> |<span data-ttu-id="d1406-330">從呼叫 toocompletion 的相依性回應時間</span><span class="sxs-lookup"><span data-stu-id="d1406-330">Time from call toocompletion of response by dependency</span></span> |
| <span data-ttu-id="d1406-331">remoteDependency [0] id</span><span class="sxs-lookup"><span data-stu-id="d1406-331">remoteDependency [0] id</span></span> |<span data-ttu-id="d1406-332">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-332">string</span></span> | |
| <span data-ttu-id="d1406-333">remoteDependency [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="d1406-333">remoteDependency [0] name</span></span> |<span data-ttu-id="d1406-334">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-334">string</span></span> |<span data-ttu-id="d1406-335">Url。</span><span class="sxs-lookup"><span data-stu-id="d1406-335">Url.</span></span> <span data-ttu-id="d1406-336">最大長度 250。</span><span class="sxs-lookup"><span data-stu-id="d1406-336">Max length 250.</span></span> |
| <span data-ttu-id="d1406-337">remoteDependency [0] resultCode</span><span class="sxs-lookup"><span data-stu-id="d1406-337">remoteDependency [0] resultCode</span></span> |<span data-ttu-id="d1406-338">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-338">string</span></span> |<span data-ttu-id="d1406-339">從 HTTP 相依性</span><span class="sxs-lookup"><span data-stu-id="d1406-339">from HTTP dependency</span></span> |
| <span data-ttu-id="d1406-340">remoteDependency [0] 成功</span><span class="sxs-lookup"><span data-stu-id="d1406-340">remoteDependency [0] success</span></span> |<span data-ttu-id="d1406-341">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-341">boolean</span></span> | |
| <span data-ttu-id="d1406-342">remoteDependency [0] 類型</span><span class="sxs-lookup"><span data-stu-id="d1406-342">remoteDependency [0] type</span></span> |<span data-ttu-id="d1406-343">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-343">string</span></span> |<span data-ttu-id="d1406-344">Http、Sql、...</span><span class="sxs-lookup"><span data-stu-id="d1406-344">Http, Sql,...</span></span> |
| <span data-ttu-id="d1406-345">remoteDependency [0] url</span><span class="sxs-lookup"><span data-stu-id="d1406-345">remoteDependency [0] url</span></span> |<span data-ttu-id="d1406-346">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-346">string</span></span> |<span data-ttu-id="d1406-347">最大長度 2000</span><span class="sxs-lookup"><span data-stu-id="d1406-347">Max length 2000</span></span> |
| <span data-ttu-id="d1406-348">remoteDependency [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="d1406-348">remoteDependency [0] urlData.base</span></span> |<span data-ttu-id="d1406-349">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-349">string</span></span> |<span data-ttu-id="d1406-350">最大長度 2000</span><span class="sxs-lookup"><span data-stu-id="d1406-350">Max length 2000</span></span> |
| <span data-ttu-id="d1406-351">remoteDependency [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="d1406-351">remoteDependency [0] urlData.hashTag</span></span> |<span data-ttu-id="d1406-352">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-352">string</span></span> | |
| <span data-ttu-id="d1406-353">remoteDependency [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="d1406-353">remoteDependency [0] urlData.host</span></span> |<span data-ttu-id="d1406-354">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-354">string</span></span> |<span data-ttu-id="d1406-355">最大長度 200</span><span class="sxs-lookup"><span data-stu-id="d1406-355">Max length 200</span></span> |

## <a name="requests"></a><span data-ttu-id="d1406-356">要求</span><span class="sxs-lookup"><span data-stu-id="d1406-356">Requests</span></span>
<span data-ttu-id="d1406-357">由 [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest)傳送。</span><span class="sxs-lookup"><span data-stu-id="d1406-357">Sent by [TrackRequest](app-insights-api-custom-events-metrics.md#trackrequest).</span></span> <span data-ttu-id="d1406-358">hello 標準模組使用此 tooreports 伺服器回應時間，測量 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1406-358">hello standard modules use this tooreports server response time, measured at hello server.</span></span>

| <span data-ttu-id="d1406-359">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-359">Path</span></span> | <span data-ttu-id="d1406-360">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-360">Type</span></span> | <span data-ttu-id="d1406-361">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-361">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-362">要求 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="d1406-362">request [0] count</span></span> |<span data-ttu-id="d1406-363">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-363">integer</span></span> |<span data-ttu-id="d1406-364">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="d1406-364">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="d1406-365">例如：4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="d1406-365">For example: 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="d1406-366">要求 [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="d1406-366">request [0] durationMetric.value</span></span> |<span data-ttu-id="d1406-367">number</span><span class="sxs-lookup"><span data-stu-id="d1406-367">number</span></span> |<span data-ttu-id="d1406-368">從要求抵達 tooresponse 時間。</span><span class="sxs-lookup"><span data-stu-id="d1406-368">Time from request arriving tooresponse.</span></span> <span data-ttu-id="d1406-369">1e7 == 1s</span><span class="sxs-lookup"><span data-stu-id="d1406-369">1e7 == 1s</span></span> |
| <span data-ttu-id="d1406-370">要求 [0] id</span><span class="sxs-lookup"><span data-stu-id="d1406-370">request [0] id</span></span> |<span data-ttu-id="d1406-371">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-371">string</span></span> |<span data-ttu-id="d1406-372">作業 id</span><span class="sxs-lookup"><span data-stu-id="d1406-372">Operation id</span></span> |
| <span data-ttu-id="d1406-373">要求 [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="d1406-373">request [0] name</span></span> |<span data-ttu-id="d1406-374">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-374">string</span></span> |<span data-ttu-id="d1406-375">GET/POST + url 基底。</span><span class="sxs-lookup"><span data-stu-id="d1406-375">GET/POST + url base.</span></span>  <span data-ttu-id="d1406-376">最大長度 250</span><span class="sxs-lookup"><span data-stu-id="d1406-376">Max length 250</span></span> |
| <span data-ttu-id="d1406-377">要求 [0] responseCode</span><span class="sxs-lookup"><span data-stu-id="d1406-377">request [0] responseCode</span></span> |<span data-ttu-id="d1406-378">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-378">integer</span></span> |<span data-ttu-id="d1406-379">HTTP 傳送回應 tooclient</span><span class="sxs-lookup"><span data-stu-id="d1406-379">HTTP response sent tooclient</span></span> |
| <span data-ttu-id="d1406-380">要求 [0] 成功</span><span class="sxs-lookup"><span data-stu-id="d1406-380">request [0] success</span></span> |<span data-ttu-id="d1406-381">布林值</span><span class="sxs-lookup"><span data-stu-id="d1406-381">boolean</span></span> |<span data-ttu-id="d1406-382">預設值 == (responseCode &lt; 400)</span><span class="sxs-lookup"><span data-stu-id="d1406-382">Default == (responseCode &lt; 400)</span></span> |
| <span data-ttu-id="d1406-383">要求 [0] url</span><span class="sxs-lookup"><span data-stu-id="d1406-383">request [0] url</span></span> |<span data-ttu-id="d1406-384">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-384">string</span></span> |<span data-ttu-id="d1406-385">不包括主機</span><span class="sxs-lookup"><span data-stu-id="d1406-385">Not including host</span></span> |
| <span data-ttu-id="d1406-386">要求 [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="d1406-386">request [0] urlData.base</span></span> |<span data-ttu-id="d1406-387">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-387">string</span></span> | |
| <span data-ttu-id="d1406-388">要求 [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="d1406-388">request [0] urlData.hashTag</span></span> |<span data-ttu-id="d1406-389">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-389">string</span></span> | |
| <span data-ttu-id="d1406-390">要求 [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="d1406-390">request [0] urlData.host</span></span> |<span data-ttu-id="d1406-391">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-391">string</span></span> | |

## <a name="page-view-performance"></a><span data-ttu-id="d1406-392">頁面檢視效能</span><span class="sxs-lookup"><span data-stu-id="d1406-392">Page View Performance</span></span>
<span data-ttu-id="d1406-393">傳送嗨瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="d1406-393">Sent by hello browser.</span></span> <span data-ttu-id="d1406-394">量值 hello 時間 tooprocess 頁面上，從使用者起始 hello 要求 toodisplay 完成 （不包括非同步 AJAX 呼叫）。</span><span class="sxs-lookup"><span data-stu-id="d1406-394">Measures hello time tooprocess a page, from user initiating hello request toodisplay complete (excluding async AJAX calls).</span></span>

<span data-ttu-id="d1406-395">內容值會顯示用戶端作業系統和瀏覽器版本。</span><span class="sxs-lookup"><span data-stu-id="d1406-395">Context values show client OS and browser version.</span></span>

| <span data-ttu-id="d1406-396">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-396">Path</span></span> | <span data-ttu-id="d1406-397">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-397">Type</span></span> | <span data-ttu-id="d1406-398">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-398">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-399">clientPerformance [0] clientProcess.value</span><span class="sxs-lookup"><span data-stu-id="d1406-399">clientPerformance [0] clientProcess.value</span></span> |<span data-ttu-id="d1406-400">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-400">integer</span></span> |<span data-ttu-id="d1406-401">從接收 hello HTML toodisplaying hello 網頁的結束時間。</span><span class="sxs-lookup"><span data-stu-id="d1406-401">Time from end of receiving hello HTML toodisplaying hello page.</span></span> |
| <span data-ttu-id="d1406-402">clientPerformance [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="d1406-402">clientPerformance [0] name</span></span> |<span data-ttu-id="d1406-403">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-403">string</span></span> | |
| <span data-ttu-id="d1406-404">clientPerformance [0] networkConnection.value</span><span class="sxs-lookup"><span data-stu-id="d1406-404">clientPerformance [0] networkConnection.value</span></span> |<span data-ttu-id="d1406-405">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-405">integer</span></span> |<span data-ttu-id="d1406-406">所花費時間 tooestablish 網路連線。</span><span class="sxs-lookup"><span data-stu-id="d1406-406">Time taken tooestablish a network connection.</span></span> |
| <span data-ttu-id="d1406-407">clientPerformance [0] receiveRequest.value</span><span class="sxs-lookup"><span data-stu-id="d1406-407">clientPerformance [0] receiveRequest.value</span></span> |<span data-ttu-id="d1406-408">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-408">integer</span></span> |<span data-ttu-id="d1406-409">從在回覆傳送嗨要求 tooreceiving hello HTML 的結束時間。</span><span class="sxs-lookup"><span data-stu-id="d1406-409">Time from end of sending hello request tooreceiving hello HTML in reply.</span></span> |
| <span data-ttu-id="d1406-410">clientPerformance [0] sendRequest.value</span><span class="sxs-lookup"><span data-stu-id="d1406-410">clientPerformance [0] sendRequest.value</span></span> |<span data-ttu-id="d1406-411">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-411">integer</span></span> |<span data-ttu-id="d1406-412">從拍攝的 toosend hello HTTP 要求的時間。</span><span class="sxs-lookup"><span data-stu-id="d1406-412">Time from taken toosend hello HTTP request.</span></span> |
| <span data-ttu-id="d1406-413">clientPerformance [0] total.value</span><span class="sxs-lookup"><span data-stu-id="d1406-413">clientPerformance [0] total.value</span></span> |<span data-ttu-id="d1406-414">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-414">integer</span></span> |<span data-ttu-id="d1406-415">無法啟動 toosend hello 要求 toodisplaying hello 頁面上的時間。</span><span class="sxs-lookup"><span data-stu-id="d1406-415">Time from starting toosend hello request toodisplaying hello page.</span></span> |
| <span data-ttu-id="d1406-416">clientPerformance [0] url</span><span class="sxs-lookup"><span data-stu-id="d1406-416">clientPerformance [0] url</span></span> |<span data-ttu-id="d1406-417">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-417">string</span></span> |<span data-ttu-id="d1406-418">此要求的 URL</span><span class="sxs-lookup"><span data-stu-id="d1406-418">URL of this request</span></span> |
| <span data-ttu-id="d1406-419">clientPerformance [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="d1406-419">clientPerformance [0] urlData.base</span></span> |<span data-ttu-id="d1406-420">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-420">string</span></span> | |
| <span data-ttu-id="d1406-421">clientPerformance [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="d1406-421">clientPerformance [0] urlData.hashTag</span></span> |<span data-ttu-id="d1406-422">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-422">string</span></span> | |
| <span data-ttu-id="d1406-423">clientPerformance [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="d1406-423">clientPerformance [0] urlData.host</span></span> |<span data-ttu-id="d1406-424">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-424">string</span></span> | |
| <span data-ttu-id="d1406-425">clientPerformance [0] urlData.protocol</span><span class="sxs-lookup"><span data-stu-id="d1406-425">clientPerformance [0] urlData.protocol</span></span> |<span data-ttu-id="d1406-426">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-426">string</span></span> | |

## <a name="page-views"></a><span data-ttu-id="d1406-427">頁面檢視</span><span class="sxs-lookup"><span data-stu-id="d1406-427">Page Views</span></span>
<span data-ttu-id="d1406-428">由 trackPageView() 或 [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views) 傳送</span><span class="sxs-lookup"><span data-stu-id="d1406-428">Sent by trackPageView() or [stopTrackPage](app-insights-api-custom-events-metrics.md#page-views)</span></span>

| <span data-ttu-id="d1406-429">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-429">Path</span></span> | <span data-ttu-id="d1406-430">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-430">Type</span></span> | <span data-ttu-id="d1406-431">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-431">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-432">檢視 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="d1406-432">view [0] count</span></span> |<span data-ttu-id="d1406-433">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-433">integer</span></span> |<span data-ttu-id="d1406-434">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="d1406-434">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="d1406-435">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="d1406-435">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="d1406-436">檢視 [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="d1406-436">view [0] durationMetric.value</span></span> |<span data-ttu-id="d1406-437">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-437">integer</span></span> |<span data-ttu-id="d1406-438">在 trackPageView() 中或由 startTrackPage() - stopTrackPage() 選擇性設定的值。</span><span class="sxs-lookup"><span data-stu-id="d1406-438">Value optionally set in trackPageView() or by startTrackPage() - stopTrackPage().</span></span> <span data-ttu-id="d1406-439">無法為 clientPerformance 值 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="d1406-439">Not hello same as clientPerformance values.</span></span> |
| <span data-ttu-id="d1406-440">檢視 [0] 名稱</span><span class="sxs-lookup"><span data-stu-id="d1406-440">view [0] name</span></span> |<span data-ttu-id="d1406-441">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-441">string</span></span> |<span data-ttu-id="d1406-442">頁面標題。</span><span class="sxs-lookup"><span data-stu-id="d1406-442">Page title.</span></span>  <span data-ttu-id="d1406-443">最大長度 250</span><span class="sxs-lookup"><span data-stu-id="d1406-443">Max length 250</span></span> |
| <span data-ttu-id="d1406-444">檢視 [0] url</span><span class="sxs-lookup"><span data-stu-id="d1406-444">view [0] url</span></span> |<span data-ttu-id="d1406-445">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-445">string</span></span> | |
| <span data-ttu-id="d1406-446">檢視 [0] urlData.base</span><span class="sxs-lookup"><span data-stu-id="d1406-446">view [0] urlData.base</span></span> |<span data-ttu-id="d1406-447">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-447">string</span></span> | |
| <span data-ttu-id="d1406-448">檢視 [0] urlData.hashTag</span><span class="sxs-lookup"><span data-stu-id="d1406-448">view [0] urlData.hashTag</span></span> |<span data-ttu-id="d1406-449">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-449">string</span></span> | |
| <span data-ttu-id="d1406-450">檢視 [0] urlData.host</span><span class="sxs-lookup"><span data-stu-id="d1406-450">view [0] urlData.host</span></span> |<span data-ttu-id="d1406-451">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-451">string</span></span> | |

## <a name="availability"></a><span data-ttu-id="d1406-452">Availability</span><span class="sxs-lookup"><span data-stu-id="d1406-452">Availability</span></span>
<span data-ttu-id="d1406-453">回報 [可用性 Web 測試](app-insights-monitor-web-app-availability.md)。</span><span class="sxs-lookup"><span data-stu-id="d1406-453">Reports [availability web tests](app-insights-monitor-web-app-availability.md).</span></span>

| <span data-ttu-id="d1406-454">Path</span><span class="sxs-lookup"><span data-stu-id="d1406-454">Path</span></span> | <span data-ttu-id="d1406-455">類型</span><span class="sxs-lookup"><span data-stu-id="d1406-455">Type</span></span> | <span data-ttu-id="d1406-456">注意事項</span><span class="sxs-lookup"><span data-stu-id="d1406-456">Notes</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d1406-457">可用性 [0] availabilityMetric.name</span><span class="sxs-lookup"><span data-stu-id="d1406-457">availability [0] availabilityMetric.name</span></span> |<span data-ttu-id="d1406-458">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-458">string</span></span> |<span data-ttu-id="d1406-459">Availability</span><span class="sxs-lookup"><span data-stu-id="d1406-459">availability</span></span> |
| <span data-ttu-id="d1406-460">可用性 [0] availabilityMetric.value</span><span class="sxs-lookup"><span data-stu-id="d1406-460">availability [0] availabilityMetric.value</span></span> |<span data-ttu-id="d1406-461">number</span><span class="sxs-lookup"><span data-stu-id="d1406-461">number</span></span> |<span data-ttu-id="d1406-462">1.0 或 0.0</span><span class="sxs-lookup"><span data-stu-id="d1406-462">1.0 or 0.0</span></span> |
| <span data-ttu-id="d1406-463">可用性 [0] 計數</span><span class="sxs-lookup"><span data-stu-id="d1406-463">availability [0] count</span></span> |<span data-ttu-id="d1406-464">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-464">integer</span></span> |<span data-ttu-id="d1406-465">100/([取樣](app-insights-sampling.md) 率)。</span><span class="sxs-lookup"><span data-stu-id="d1406-465">100/([sampling](app-insights-sampling.md) rate).</span></span> <span data-ttu-id="d1406-466">例如 4 =&gt; 25%。</span><span class="sxs-lookup"><span data-stu-id="d1406-466">For example 4 =&gt; 25%.</span></span> |
| <span data-ttu-id="d1406-467">可用性 [0] dataSizeMetric.name</span><span class="sxs-lookup"><span data-stu-id="d1406-467">availability [0] dataSizeMetric.name</span></span> |<span data-ttu-id="d1406-468">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-468">string</span></span> | |
| <span data-ttu-id="d1406-469">可用性 [0] dataSizeMetric.value</span><span class="sxs-lookup"><span data-stu-id="d1406-469">availability [0] dataSizeMetric.value</span></span> |<span data-ttu-id="d1406-470">integer</span><span class="sxs-lookup"><span data-stu-id="d1406-470">integer</span></span> | |
| <span data-ttu-id="d1406-471">可用性 [0] durationMetric.name</span><span class="sxs-lookup"><span data-stu-id="d1406-471">availability [0] durationMetric.name</span></span> |<span data-ttu-id="d1406-472">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-472">string</span></span> | |
| <span data-ttu-id="d1406-473">可用性 [0] durationMetric.value</span><span class="sxs-lookup"><span data-stu-id="d1406-473">availability [0] durationMetric.value</span></span> |<span data-ttu-id="d1406-474">number</span><span class="sxs-lookup"><span data-stu-id="d1406-474">number</span></span> |<span data-ttu-id="d1406-475">測試持續時間。</span><span class="sxs-lookup"><span data-stu-id="d1406-475">Duration of test.</span></span> <span data-ttu-id="d1406-476">1e7==1s</span><span class="sxs-lookup"><span data-stu-id="d1406-476">1e7==1s</span></span> |
| <span data-ttu-id="d1406-477">可用性 [0] 訊息</span><span class="sxs-lookup"><span data-stu-id="d1406-477">availability [0] message</span></span> |<span data-ttu-id="d1406-478">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-478">string</span></span> |<span data-ttu-id="d1406-479">失敗診斷</span><span class="sxs-lookup"><span data-stu-id="d1406-479">Failure diagnostic</span></span> |
| <span data-ttu-id="d1406-480">可用性 [0] 結果</span><span class="sxs-lookup"><span data-stu-id="d1406-480">availability [0] result</span></span> |<span data-ttu-id="d1406-481">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-481">string</span></span> |<span data-ttu-id="d1406-482">通過/失敗</span><span class="sxs-lookup"><span data-stu-id="d1406-482">Pass/Fail</span></span> |
| <span data-ttu-id="d1406-483">可用性 [0] runLocation</span><span class="sxs-lookup"><span data-stu-id="d1406-483">availability [0] runLocation</span></span> |<span data-ttu-id="d1406-484">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-484">string</span></span> |<span data-ttu-id="d1406-485">http req 的地理區域來源</span><span class="sxs-lookup"><span data-stu-id="d1406-485">Geo source of http req</span></span> |
| <span data-ttu-id="d1406-486">可用性 [0] testName</span><span class="sxs-lookup"><span data-stu-id="d1406-486">availability [0] testName</span></span> |<span data-ttu-id="d1406-487">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-487">string</span></span> | |
| <span data-ttu-id="d1406-488">可用性 [0] testRunId</span><span class="sxs-lookup"><span data-stu-id="d1406-488">availability [0] testRunId</span></span> |<span data-ttu-id="d1406-489">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-489">string</span></span> | |
| <span data-ttu-id="d1406-490">可用性 [0] testTimestamp</span><span class="sxs-lookup"><span data-stu-id="d1406-490">availability [0] testTimestamp</span></span> |<span data-ttu-id="d1406-491">字串</span><span class="sxs-lookup"><span data-stu-id="d1406-491">string</span></span> | |

## <a name="metrics"></a><span data-ttu-id="d1406-492">度量</span><span class="sxs-lookup"><span data-stu-id="d1406-492">Metrics</span></span>
<span data-ttu-id="d1406-493">由 TrackMetric() 產生。</span><span class="sxs-lookup"><span data-stu-id="d1406-493">Generated by TrackMetric().</span></span>

<span data-ttu-id="d1406-494">hello 公制值位於 context.custom.metrics[0]</span><span class="sxs-lookup"><span data-stu-id="d1406-494">hello metric value is found in context.custom.metrics[0]</span></span>

<span data-ttu-id="d1406-495">例如：</span><span class="sxs-lookup"><span data-stu-id="d1406-495">For example:</span></span>

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

## <a name="about-metric-values"></a><span data-ttu-id="d1406-496">關於度量值</span><span class="sxs-lookup"><span data-stu-id="d1406-496">About metric values</span></span>
<span data-ttu-id="d1406-497">在度量報告和其他位置中的度量值，會利用標準物件結構回報。</span><span class="sxs-lookup"><span data-stu-id="d1406-497">Metric values, both in metric reports and elsewhere, are reported with a standard object structure.</span></span> <span data-ttu-id="d1406-498">例如：</span><span class="sxs-lookup"><span data-stu-id="d1406-498">For example:</span></span>

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

<span data-ttu-id="d1406-499">目前-但這可能會變更在未來-從標準 SDK 模組 hello，回報的所有值中的 hello`count==1`只 hello 和`name`和`value`欄位很有用。</span><span class="sxs-lookup"><span data-stu-id="d1406-499">Currently - though this might change in hello future - in all values reported from hello standard SDK modules, `count==1` and only hello `name` and `value` fields are useful.</span></span> <span data-ttu-id="d1406-500">hello，其方式是不同的唯一情況是如果您撰寫您自己的 TrackMetric 呼叫用以設定 hello 其他參數。</span><span class="sxs-lookup"><span data-stu-id="d1406-500">hello only case where they would be different would be if you write your own TrackMetric calls in which you set hello other parameters.</span></span>

<span data-ttu-id="d1406-501">hello 用途 hello 的其他欄位是 tooallow 度量 toobe hello SDK，tooreduce 流量 toohello 入口網站中的彙總資料。</span><span class="sxs-lookup"><span data-stu-id="d1406-501">hello purpose of hello other fields is tooallow metrics toobe aggregated in hello SDK, tooreduce traffic toohello portal.</span></span> <span data-ttu-id="d1406-502">例如，您可以在傳送每個度量報告之前平均數個連續的讀數。</span><span class="sxs-lookup"><span data-stu-id="d1406-502">For example, you could average several successive readings before sending each metric report.</span></span> <span data-ttu-id="d1406-503">然後會計算 hello min、 max、 標準差和彙總 （sum 或 average） 的值，並設定讀數 hello 報表所代表的計數 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="d1406-503">Then you would calculate hello min, max, standard deviation and aggregate value (sum or average) and set count toohello number of readings represented by hello report.</span></span>

<span data-ttu-id="d1406-504">在上述的 hello 表格，我們省略 hello 很少使用的欄位 count、 min、 max、 標準差和 sampledValue。</span><span class="sxs-lookup"><span data-stu-id="d1406-504">In hello tables above, we have omitted hello rarely-used fields count, min, max, stdDev and sampledValue.</span></span>

<span data-ttu-id="d1406-505">您可以使用預先彙總的度量，代替[取樣](app-insights-sampling.md)如果您需要 tooreduce hello 磁碟區的遙測資料。</span><span class="sxs-lookup"><span data-stu-id="d1406-505">Instead of pre-aggregating metrics, you can use [sampling](app-insights-sampling.md) if you need tooreduce hello volume of telemetry.</span></span>

### <a name="durations"></a><span data-ttu-id="d1406-506">持續時間</span><span class="sxs-lookup"><span data-stu-id="d1406-506">Durations</span></span>
<span data-ttu-id="d1406-507">除非另有說明，否則持續時間皆以十分之一微秒表示，所以 10000000.0 表示 1 秒。</span><span class="sxs-lookup"><span data-stu-id="d1406-507">Except where otherwise noted, durations are represented in tenths of a microsecond, so that 10000000.0 means 1 second.</span></span>

## <a name="see-also"></a><span data-ttu-id="d1406-508">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d1406-508">See also</span></span>
* [<span data-ttu-id="d1406-509">Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1406-509">Application Insights</span></span>](app-insights-overview.md)
* [<span data-ttu-id="d1406-510">連續匯出</span><span class="sxs-lookup"><span data-stu-id="d1406-510">Continuous Export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="d1406-511">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d1406-511">Code samples</span></span>](app-insights-export-telemetry.md#code-samples)
