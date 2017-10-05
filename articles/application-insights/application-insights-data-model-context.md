---
title: "Azure Application Insights 遙測資料模型 - 遙測內容 | Microsoft Docs"
description: "Application Insights 遙測內容資料模型"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/15/2017
ms.author: sergkanz
ms.openlocfilehash: d6a0cad8bda6ca68aa691867e84f540c5ac9f6f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="9d2d5-103">遙測內容：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="9d2d5-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="9d2d5-104">每個遙測項目都可能具有強型別的內容欄位。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="9d2d5-105">每個欄位都具有特定的監視案例。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="9d2d5-106">請使用自訂屬性集合來儲存自訂或應用程式特定的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-106">Use the custom properties collection to store custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="9d2d5-107">應用程式版本</span><span class="sxs-lookup"><span data-stu-id="9d2d5-107">Application version</span></span>

<span data-ttu-id="9d2d5-108">應用程式內容欄位中一律是與傳送遙測之應用程式相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-108">Information in the application context fields is always about the application that is sending the telemetry.</span></span> <span data-ttu-id="9d2d5-109">應用程式版本可用於分析應用程式行為及其與部署相互關聯中的趨勢變更。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-109">Application version is used to analyze trend changes in the application behavior and its correlation to the deployments.</span></span>

<span data-ttu-id="9d2d5-110">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="9d2d5-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="9d2d5-111">用戶端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="9d2d5-111">Client IP address</span></span>

<span data-ttu-id="9d2d5-112">用戶端裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-112">The IP address of the client device.</span></span> <span data-ttu-id="9d2d5-113">支援 IPv4 和 IPv6。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="9d2d5-114">從服務傳送遙測時，位置內容與服務中起始作業的使用者相關。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-114">When telemetry is sent from a service, the location context is about the user that initiated the operation in the service.</span></span> <span data-ttu-id="9d2d5-115">Application Insights 會從用戶端 IP 擷取地理位置資訊並予以截斷。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-115">Application Insights extract the geo-location information from the client IP and then truncate it.</span></span> <span data-ttu-id="9d2d5-116">因此用戶端 IP 本身無法作為終端使用者識別資訊。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="9d2d5-117">最大長度：46</span><span class="sxs-lookup"><span data-stu-id="9d2d5-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="9d2d5-118">裝置類型</span><span class="sxs-lookup"><span data-stu-id="9d2d5-118">Device type</span></span>

<span data-ttu-id="9d2d5-119">原本此欄位是用於表示應用程式終端使用者正在使用的裝置類型。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-119">Originally this field was used to indicate the type of the device the end user of the application is using.</span></span> <span data-ttu-id="9d2d5-120">目前主要用於區別裝置類型為「瀏覽器」的 JavaScript 遙測與裝置類型為「電腦」的伺服器端遙測。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-120">Today used primarily to distinguish JavaScript telemetry with the device type 'Browser' from server-side telemetry with the device type 'PC'.</span></span>

<span data-ttu-id="9d2d5-121">最大長度：64</span><span class="sxs-lookup"><span data-stu-id="9d2d5-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="9d2d5-122">作業 id</span><span class="sxs-lookup"><span data-stu-id="9d2d5-122">Operation id</span></span>

<span data-ttu-id="9d2d5-123">根作業的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-123">A unique identifier of the root operation.</span></span> <span data-ttu-id="9d2d5-124">此識別碼可讓群組遙測跨越多個元件。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-124">This identifier allows to group telemetry across multiple components.</span></span> <span data-ttu-id="9d2d5-125">如需詳細資訊，請參閱[遙測相互關聯](application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="9d2d5-126">作業識別碼會由要求或頁面檢視所建立。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-126">The operation id is created by either a request or a page view.</span></span> <span data-ttu-id="9d2d5-127">所有其他遙測會將此欄位設定為包含要求或頁面檢視的值。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-127">All other telemetry sets this field to the value for the containing request or page view.</span></span> 

<span data-ttu-id="9d2d5-128">最大長度：128</span><span class="sxs-lookup"><span data-stu-id="9d2d5-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="9d2d5-129">父作業識別碼</span><span class="sxs-lookup"><span data-stu-id="9d2d5-129">Parent operation ID</span></span>

<span data-ttu-id="9d2d5-130">遙測項目直屬父代的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-130">The unique identifier of the telemetry item's immediate parent.</span></span> <span data-ttu-id="9d2d5-131">如需詳細資訊，請參閱[遙測相互關聯](application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="9d2d5-132">最大長度：128</span><span class="sxs-lookup"><span data-stu-id="9d2d5-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="9d2d5-133">作業名稱</span><span class="sxs-lookup"><span data-stu-id="9d2d5-133">Operation name</span></span>

<span data-ttu-id="9d2d5-134">作業的名稱 (群組)。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-134">The name (group) of the operation.</span></span> <span data-ttu-id="9d2d5-135">作業名稱會由要求或頁面檢視所建立。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-135">The operation name is created by either a request or a page view.</span></span> <span data-ttu-id="9d2d5-136">所有其他遙測項目會將此欄位設定為包含要求或頁面檢視的值。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-136">All other telemetry items set this field to the value for the containing request or page view.</span></span> <span data-ttu-id="9d2d5-137">作業名稱可用於尋找作業群組的所有遙測項目 (例如 'GET Home/Index')。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-137">Operation name is used for finding all the telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="9d2d5-138">此內容屬性可用於回答「此頁面擲回的一般例外狀況為何」等問題。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-138">This context property is used to answer questions like "what are the typical exceptions thrown on this page."</span></span>

<span data-ttu-id="9d2d5-139">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="9d2d5-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-the-operation"></a><span data-ttu-id="9d2d5-140">作業的綜合來源</span><span class="sxs-lookup"><span data-stu-id="9d2d5-140">Synthetic source of the operation</span></span>

<span data-ttu-id="9d2d5-141">綜合來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-141">Name of synthetic source.</span></span> <span data-ttu-id="9d2d5-142">來自可能代表綜合流量之應用程式的一些遙測。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-142">Some telemetry from the application may represent synthetic traffic.</span></span> <span data-ttu-id="9d2d5-143">其可能是來自 Application Insights SDK 本身等診斷程式庫之編製網站索引的網頁編目程式、網站可用性測試或追蹤。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-143">It may be web crawler indexing the web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="9d2d5-144">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="9d2d5-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="9d2d5-145">工作階段識別碼</span><span class="sxs-lookup"><span data-stu-id="9d2d5-145">Session id</span></span>

<span data-ttu-id="9d2d5-146">工作階段識別碼 - 與應用程式進行使用者互動的執行個體。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-146">Session ID - the instance of the user's interaction with the app.</span></span> <span data-ttu-id="9d2d5-147">工作階段內容欄位中一律是與終端使用者相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-147">Information in the session context fields is always about the end user.</span></span> <span data-ttu-id="9d2d5-148">從服務傳送遙測時，工作階段內容與服務中起始作業的使用者相關。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-148">When telemetry is sent from a service, the session context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="9d2d5-149">最大長度：64</span><span class="sxs-lookup"><span data-stu-id="9d2d5-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="9d2d5-150">匿名使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="9d2d5-150">Anonymous user id</span></span>

<span data-ttu-id="9d2d5-151">匿名使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-151">Anonymous user id.</span></span> <span data-ttu-id="9d2d5-152">代表應用程式的終端使用者。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-152">Represents the end user of the application.</span></span> <span data-ttu-id="9d2d5-153">從服務傳送遙測時，使用者內容與服務中起始作業的使用者相關。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-153">When telemetry is sent from a service, the user context is about the user that initiated the operation in the service.</span></span>

<span data-ttu-id="9d2d5-154">[取樣](app-insights-sampling.md)是將收集的遙測量降到最低的其中一個方法。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-154">[Sampling](app-insights-sampling.md) is one of the techniques to minimize the amount of collected telemetry.</span></span> <span data-ttu-id="9d2d5-155">取樣演算法會嘗試取樣輸入或輸出所有相互關聯的遙測。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-155">Sampling algorithm attempts to either sample in or out all the correlated telemetry.</span></span> <span data-ttu-id="9d2d5-156">匿名使用者識別碼可用於產生取樣分數。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-156">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="9d2d5-157">因此匿名使用者識別碼應該為足夠隨機的值。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-157">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="9d2d5-158">使用匿名使用者識別碼儲存使用者名稱是濫用欄位的做法。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-158">Using anonymous user id to store user name is a misuse of the field.</span></span> <span data-ttu-id="9d2d5-159">使用已驗證的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-159">Use Authenticated user id.</span></span>

<span data-ttu-id="9d2d5-160">最大長度：128</span><span class="sxs-lookup"><span data-stu-id="9d2d5-160">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="9d2d5-161">已驗證的使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="9d2d5-161">Authenticated user id</span></span>

<span data-ttu-id="9d2d5-162">已驗證的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-162">Authenticated user id.</span></span> <span data-ttu-id="9d2d5-163">與匿名使用者識別碼相反，此欄位代表具有易記名稱的使用者。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-163">The opposite of anonymous user id, this field represents the user with a friendly name.</span></span> <span data-ttu-id="9d2d5-164">由於其 PII 資訊，根據預設，大部分的 SDK 都不會收集該資訊。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-164">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="9d2d5-165">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="9d2d5-165">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="9d2d5-166">帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="9d2d5-166">Account id</span></span>

<span data-ttu-id="9d2d5-167">在多租用戶應用程式中，此為使用者使用的帳戶識別碼或名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-167">In multi-tenant applications this is the account ID or name, which the user is acting with.</span></span> <span data-ttu-id="9d2d5-168">範例包括 Azure 入口網站的訂用帳戶識別碼或部落格平台的部落格名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-168">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="9d2d5-169">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="9d2d5-169">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="9d2d5-170">雲端角色</span><span class="sxs-lookup"><span data-stu-id="9d2d5-170">Cloud role</span></span>

<span data-ttu-id="9d2d5-171">應用程式角色的名稱是其中的一部分。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-171">Name of the role the application is a part of.</span></span> <span data-ttu-id="9d2d5-172">在 Azure 中直接對應到角色名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-172">Maps directly to the role name in azure.</span></span> <span data-ttu-id="9d2d5-173">您也可以將其用於區別微服務，其為單一應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-173">Can also be used to distinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="9d2d5-174">最大長度：256</span><span class="sxs-lookup"><span data-stu-id="9d2d5-174">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="9d2d5-175">雲端角色執行個體</span><span class="sxs-lookup"><span data-stu-id="9d2d5-175">Cloud role instance</span></span>

<span data-ttu-id="9d2d5-176">執行應用程式的執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-176">Name of the instance where the application is running.</span></span> <span data-ttu-id="9d2d5-177">內部部署的電腦名稱、Azure 的執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-177">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="9d2d5-178">最大長度：256</span><span class="sxs-lookup"><span data-stu-id="9d2d5-178">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="9d2d5-179">內部：SDK 版本</span><span class="sxs-lookup"><span data-stu-id="9d2d5-179">Internal: SDK version</span></span>

<span data-ttu-id="9d2d5-180">SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-180">SDK version.</span></span> <span data-ttu-id="9d2d5-181">如需相關資訊，請參閱 https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-181">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="9d2d5-182">最大長度：64</span><span class="sxs-lookup"><span data-stu-id="9d2d5-182">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="9d2d5-183">內部：節點名稱</span><span class="sxs-lookup"><span data-stu-id="9d2d5-183">Internal: Node name</span></span>

<span data-ttu-id="9d2d5-184">此欄位代表用於計費的節點名稱。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-184">This field represents the node name used for billing purposes.</span></span> <span data-ttu-id="9d2d5-185">您可以將其用於覆寫節點的標準偵測。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-185">Use it to override the standard detection of nodes.</span></span>

<span data-ttu-id="9d2d5-186">最大長度：256</span><span class="sxs-lookup"><span data-stu-id="9d2d5-186">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="9d2d5-187">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d2d5-187">Next steps</span></span>

- <span data-ttu-id="9d2d5-188">了解如何[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-188">Learn how to [extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="9d2d5-189">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-189">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="9d2d5-190">請查看標準內容屬性集合[組態](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)。</span><span class="sxs-lookup"><span data-stu-id="9d2d5-190">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
