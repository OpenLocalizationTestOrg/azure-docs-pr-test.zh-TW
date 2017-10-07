---
title: "aaaAzure Insights 遙測資料模型的應用程式的遙測內容 |Microsoft 文件"
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
ms.openlocfilehash: 6cdd6240d1c448f883d104a871ee9d5f6b5af2ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-context-application-insights-data-model"></a><span data-ttu-id="3b26e-103">遙測內容：Application Insights 資料模型</span><span class="sxs-lookup"><span data-stu-id="3b26e-103">Telemetry context: Application Insights data model</span></span>

<span data-ttu-id="3b26e-104">每個遙測項目都可能具有強型別的內容欄位。</span><span class="sxs-lookup"><span data-stu-id="3b26e-104">Every telemetry item may have a strongly typed context fields.</span></span> <span data-ttu-id="3b26e-105">每個欄位都具有特定的監視案例。</span><span class="sxs-lookup"><span data-stu-id="3b26e-105">Every field enables a specific monitoring scenario.</span></span> <span data-ttu-id="3b26e-106">使用 hello 自訂屬性集合 toostore 自訂或特定應用程式的內容資訊。</span><span class="sxs-lookup"><span data-stu-id="3b26e-106">Use hello custom properties collection toostore custom or application-specific contextual information.</span></span>


##<a name="application-version"></a><span data-ttu-id="3b26e-107">應用程式版本</span><span class="sxs-lookup"><span data-stu-id="3b26e-107">Application version</span></span>

<span data-ttu-id="3b26e-108">Hello 應用程式內容欄位中的資訊永遠是有關傳送嗨遙測的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3b26e-108">Information in hello application context fields is always about hello application that is sending hello telemetry.</span></span> <span data-ttu-id="3b26e-109">應用程式版本是使用的 tooanalyze 趨勢變更 hello 應用程式行為以及其相互關聯 toohello 部署。</span><span class="sxs-lookup"><span data-stu-id="3b26e-109">Application version is used tooanalyze trend changes in hello application behavior and its correlation toohello deployments.</span></span>

<span data-ttu-id="3b26e-110">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="3b26e-110">Max length: 1024</span></span>


##<a name="client-ip-address"></a><span data-ttu-id="3b26e-111">用戶端 IP 位址</span><span class="sxs-lookup"><span data-stu-id="3b26e-111">Client IP address</span></span>

<span data-ttu-id="3b26e-112">hello hello 用戶端裝置的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3b26e-112">hello IP address of hello client device.</span></span> <span data-ttu-id="3b26e-113">支援 IPv4 和 IPv6。</span><span class="sxs-lookup"><span data-stu-id="3b26e-113">IPv4 and IPv6 are supported.</span></span> <span data-ttu-id="3b26e-114">從服務傳送遙測，hello 位置內容時，關於 hello 使用者起始 hello 服務中的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b26e-114">When telemetry is sent from a service, hello location context is about hello user that initiated hello operation in hello service.</span></span> <span data-ttu-id="3b26e-115">Application Insights 從 hello 用戶端 IP 擷取 hello 地理位置資訊，並予以截斷。</span><span class="sxs-lookup"><span data-stu-id="3b26e-115">Application Insights extract hello geo-location information from hello client IP and then truncate it.</span></span> <span data-ttu-id="3b26e-116">因此用戶端 IP 本身無法作為終端使用者識別資訊。</span><span class="sxs-lookup"><span data-stu-id="3b26e-116">So client IP by itself cannot be used as end-user identifiable information.</span></span> 

<span data-ttu-id="3b26e-117">最大長度：46</span><span class="sxs-lookup"><span data-stu-id="3b26e-117">Max length: 46</span></span>


##<a name="device-type"></a><span data-ttu-id="3b26e-118">裝置類型</span><span class="sxs-lookup"><span data-stu-id="3b26e-118">Device type</span></span>

<span data-ttu-id="3b26e-119">這個欄位用最初 tooindicate hello 類型 hello 裝置 hello hello 應用程式的終端使用者使用。</span><span class="sxs-lookup"><span data-stu-id="3b26e-119">Originally this field was used tooindicate hello type of hello device hello end user of hello application is using.</span></span> <span data-ttu-id="3b26e-120">今天主要 toodistinguish JavaScript 遙測 hello 裝置類型使用 '瀏覽器' 從伺服器端遙測 hello 'PC' 的裝置類型。</span><span class="sxs-lookup"><span data-stu-id="3b26e-120">Today used primarily toodistinguish JavaScript telemetry with hello device type 'Browser' from server-side telemetry with hello device type 'PC'.</span></span>

<span data-ttu-id="3b26e-121">最大長度：64</span><span class="sxs-lookup"><span data-stu-id="3b26e-121">Max length: 64</span></span>


##<a name="operation-id"></a><span data-ttu-id="3b26e-122">作業 id</span><span class="sxs-lookup"><span data-stu-id="3b26e-122">Operation id</span></span>

<span data-ttu-id="3b26e-123">Hello 根作業的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b26e-123">A unique identifier of hello root operation.</span></span> <span data-ttu-id="3b26e-124">這個識別碼可跨多個元件，讓 toogroup 遙測。</span><span class="sxs-lookup"><span data-stu-id="3b26e-124">This identifier allows toogroup telemetry across multiple components.</span></span> <span data-ttu-id="3b26e-125">如需詳細資訊，請參閱[遙測相互關聯](application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="3b26e-125">See [telemetry correlation](application-insights-correlation.md) for details.</span></span> <span data-ttu-id="3b26e-126">hello 作業 id 會建立 要求 或 頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="3b26e-126">hello operation id is created by either a request or a page view.</span></span> <span data-ttu-id="3b26e-127">所有其他遙測設定 hello 包含要求或頁面檢視此欄位 toohello 值。</span><span class="sxs-lookup"><span data-stu-id="3b26e-127">All other telemetry sets this field toohello value for hello containing request or page view.</span></span> 

<span data-ttu-id="3b26e-128">最大長度：128</span><span class="sxs-lookup"><span data-stu-id="3b26e-128">Max length: 128</span></span>


##<a name="parent-operation-id"></a><span data-ttu-id="3b26e-129">父作業識別碼</span><span class="sxs-lookup"><span data-stu-id="3b26e-129">Parent operation ID</span></span>

<span data-ttu-id="3b26e-130">hello hello 遙測項目的直屬父系的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b26e-130">hello unique identifier of hello telemetry item's immediate parent.</span></span> <span data-ttu-id="3b26e-131">如需詳細資訊，請參閱[遙測相互關聯](application-insights-correlation.md)。</span><span class="sxs-lookup"><span data-stu-id="3b26e-131">See [telemetry correlation](application-insights-correlation.md) for details.</span></span>

<span data-ttu-id="3b26e-132">最大長度：128</span><span class="sxs-lookup"><span data-stu-id="3b26e-132">Max length: 128</span></span>


##<a name="operation-name"></a><span data-ttu-id="3b26e-133">作業名稱</span><span class="sxs-lookup"><span data-stu-id="3b26e-133">Operation name</span></span>

<span data-ttu-id="3b26e-134">hello 作業的 hello 名稱 （群組）。</span><span class="sxs-lookup"><span data-stu-id="3b26e-134">hello name (group) of hello operation.</span></span> <span data-ttu-id="3b26e-135">hello 作業名稱會建立 要求 或 頁面檢視。</span><span class="sxs-lookup"><span data-stu-id="3b26e-135">hello operation name is created by either a request or a page view.</span></span> <span data-ttu-id="3b26e-136">所有其他遙測項目欄位 toohello 將此值設定 hello 包含要求或頁面的檢視。</span><span class="sxs-lookup"><span data-stu-id="3b26e-136">All other telemetry items set this field toohello value for hello containing request or page view.</span></span> <span data-ttu-id="3b26e-137">作業名稱會尋找所有 hello 遙測項目群組的作業 (例如 ' GET Home/Index ')。</span><span class="sxs-lookup"><span data-stu-id="3b26e-137">Operation name is used for finding all hello telemetry items for a group of operations (for example 'GET Home/Index').</span></span> <span data-ttu-id="3b26e-138">這個內容屬性是使用的 tooanswer 類似 「 什麼是 hello 擲回此頁面上的一般例外狀況 」。</span><span class="sxs-lookup"><span data-stu-id="3b26e-138">This context property is used tooanswer questions like "what are hello typical exceptions thrown on this page."</span></span>

<span data-ttu-id="3b26e-139">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="3b26e-139">Max length: 1024</span></span>


##<a name="synthetic-source-of-hello-operation"></a><span data-ttu-id="3b26e-140">綜合作業來源的 hello</span><span class="sxs-lookup"><span data-stu-id="3b26e-140">Synthetic source of hello operation</span></span>

<span data-ttu-id="3b26e-141">綜合來源的名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-141">Name of synthetic source.</span></span> <span data-ttu-id="3b26e-142">某些 hello 應用程式的遙測可能代表綜合流量。</span><span class="sxs-lookup"><span data-stu-id="3b26e-142">Some telemetry from hello application may represent synthetic traffic.</span></span> <span data-ttu-id="3b26e-143">它可能 web crawler 建立索引 hello web 站台、 站台可用性測試或從診斷程式庫，例如 Application Insights SDK 本身的追蹤。</span><span class="sxs-lookup"><span data-stu-id="3b26e-143">It may be web crawler indexing hello web site, site availability tests, or traces from diagnostic libraries like Application Insights SDK itself.</span></span>

<span data-ttu-id="3b26e-144">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="3b26e-144">Max length: 1024</span></span>


##<a name="session-id"></a><span data-ttu-id="3b26e-145">工作階段識別碼</span><span class="sxs-lookup"><span data-stu-id="3b26e-145">Session id</span></span>

<span data-ttu-id="3b26e-146">工作階段識別碼 hello hello 使用者互動 hello 應用程式執行個體。</span><span class="sxs-lookup"><span data-stu-id="3b26e-146">Session ID - hello instance of hello user's interaction with hello app.</span></span> <span data-ttu-id="3b26e-147">Hello 工作階段內容欄位中的資訊永遠是關於 hello 終端使用者。</span><span class="sxs-lookup"><span data-stu-id="3b26e-147">Information in hello session context fields is always about hello end user.</span></span> <span data-ttu-id="3b26e-148">從服務傳送遙測，hello 工作階段內容時，關於 hello 使用者起始 hello 服務中的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b26e-148">When telemetry is sent from a service, hello session context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="3b26e-149">最大長度：64</span><span class="sxs-lookup"><span data-stu-id="3b26e-149">Max length: 64</span></span>


##<a name="anonymous-user-id"></a><span data-ttu-id="3b26e-150">匿名使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="3b26e-150">Anonymous user id</span></span>

<span data-ttu-id="3b26e-151">匿名使用者識別碼。代表 hello hello 應用程式的使用者。</span><span class="sxs-lookup"><span data-stu-id="3b26e-151">Anonymous user id. Represents hello end user of hello application.</span></span> <span data-ttu-id="3b26e-152">從服務傳送遙測，hello 使用者內容時，關於 hello 使用者起始 hello 服務中的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="3b26e-152">When telemetry is sent from a service, hello user context is about hello user that initiated hello operation in hello service.</span></span>

<span data-ttu-id="3b26e-153">[取樣](app-insights-sampling.md)是其中一個 hello 技術 toominimize hello 數量所收集的遙測。</span><span class="sxs-lookup"><span data-stu-id="3b26e-153">[Sampling](app-insights-sampling.md) is one of hello techniques toominimize hello amount of collected telemetry.</span></span> <span data-ttu-id="3b26e-154">取樣演算法嘗試 tooeither in 或 out 所有 hello 的範例相互關聯的遙測。</span><span class="sxs-lookup"><span data-stu-id="3b26e-154">Sampling algorithm attempts tooeither sample in or out all hello correlated telemetry.</span></span> <span data-ttu-id="3b26e-155">匿名使用者識別碼可用於產生取樣分數。</span><span class="sxs-lookup"><span data-stu-id="3b26e-155">Anonymous user id is used for sampling score generation.</span></span> <span data-ttu-id="3b26e-156">因此匿名使用者識別碼應該為足夠隨機的值。</span><span class="sxs-lookup"><span data-stu-id="3b26e-156">So anonymous user id should be a random enough value.</span></span> 

<span data-ttu-id="3b26e-157">使用匿名使用者識別碼 toostore 使用者名稱是 hello 欄位誤用。</span><span class="sxs-lookup"><span data-stu-id="3b26e-157">Using anonymous user id toostore user name is a misuse of hello field.</span></span> <span data-ttu-id="3b26e-158">使用已驗證的使用者識別碼。</span><span class="sxs-lookup"><span data-stu-id="3b26e-158">Use Authenticated user id.</span></span>

<span data-ttu-id="3b26e-159">最大長度：128</span><span class="sxs-lookup"><span data-stu-id="3b26e-159">Max length: 128</span></span>


##<a name="authenticated-user-id"></a><span data-ttu-id="3b26e-160">已驗證的使用者識別碼</span><span class="sxs-lookup"><span data-stu-id="3b26e-160">Authenticated user id</span></span>

<span data-ttu-id="3b26e-161">已驗證的使用者識別碼。相反的 hello 匿名使用者 id，這個欄位代表 hello 使用者易記名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-161">Authenticated user id. hello opposite of anonymous user id, this field represents hello user with a friendly name.</span></span> <span data-ttu-id="3b26e-162">由於其 PII 資訊，根據預設，大部分的 SDK 都不會收集該資訊。</span><span class="sxs-lookup"><span data-stu-id="3b26e-162">Since its PII information it is not collected by default by most SDK.</span></span>

<span data-ttu-id="3b26e-163">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="3b26e-163">Max length: 1024</span></span>


##<a name="account-id"></a><span data-ttu-id="3b26e-164">帳戶識別碼</span><span class="sxs-lookup"><span data-stu-id="3b26e-164">Account id</span></span>

<span data-ttu-id="3b26e-165">在多租用戶應用程式中，這是 hello 帳戶識別碼或名稱，與 hello 使用者做。</span><span class="sxs-lookup"><span data-stu-id="3b26e-165">In multi-tenant applications this is hello account ID or name, which hello user is acting with.</span></span> <span data-ttu-id="3b26e-166">範例包括 Azure 入口網站的訂用帳戶識別碼或部落格平台的部落格名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-166">Examples may be subscription ID for Azure portal or blog name blogging platform.</span></span>

<span data-ttu-id="3b26e-167">最大長度：1024</span><span class="sxs-lookup"><span data-stu-id="3b26e-167">Max length: 1024</span></span>


##<a name="cloud-role"></a><span data-ttu-id="3b26e-168">雲端角色</span><span class="sxs-lookup"><span data-stu-id="3b26e-168">Cloud role</span></span>

<span data-ttu-id="3b26e-169">Hello 角色 hello 應用程式的名稱是的一部分。</span><span class="sxs-lookup"><span data-stu-id="3b26e-169">Name of hello role hello application is a part of.</span></span> <span data-ttu-id="3b26e-170">直接對應 toohello 在 azure 中的角色名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-170">Maps directly toohello role name in azure.</span></span> <span data-ttu-id="3b26e-171">也可以使用的 toodistinguish 屬於單一應用程式中的微服務。</span><span class="sxs-lookup"><span data-stu-id="3b26e-171">Can also be used toodistinguish micro services, which are part of a single application.</span></span>

<span data-ttu-id="3b26e-172">最大長度：256</span><span class="sxs-lookup"><span data-stu-id="3b26e-172">Max length: 256</span></span>


##<a name="cloud-role-instance"></a><span data-ttu-id="3b26e-173">雲端角色執行個體</span><span class="sxs-lookup"><span data-stu-id="3b26e-173">Cloud role instance</span></span>

<span data-ttu-id="3b26e-174">Hello hello 應用程式執行所在的執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-174">Name of hello instance where hello application is running.</span></span> <span data-ttu-id="3b26e-175">內部部署的電腦名稱、Azure 的執行個體名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-175">Computer name for on-premises, instance name for Azure.</span></span>

<span data-ttu-id="3b26e-176">最大長度：256</span><span class="sxs-lookup"><span data-stu-id="3b26e-176">Max length: 256</span></span>


##<a name="internal-sdk-version"></a><span data-ttu-id="3b26e-177">內部：SDK 版本</span><span class="sxs-lookup"><span data-stu-id="3b26e-177">Internal: SDK version</span></span>

<span data-ttu-id="3b26e-178">SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="3b26e-178">SDK version.</span></span> <span data-ttu-id="3b26e-179">如需相關資訊，請參閱 https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification。</span><span class="sxs-lookup"><span data-stu-id="3b26e-179">See https://github.com/Microsoft/ApplicationInsights-Home/blob/master/SDK-AUTHORING.md#sdk-version-specification for information.</span></span>

<span data-ttu-id="3b26e-180">最大長度：64</span><span class="sxs-lookup"><span data-stu-id="3b26e-180">Max length: 64</span></span>


##<a name="internal-node-name"></a><span data-ttu-id="3b26e-181">內部：節點名稱</span><span class="sxs-lookup"><span data-stu-id="3b26e-181">Internal: Node name</span></span>

<span data-ttu-id="3b26e-182">此欄位會顯示用來進行計費的 hello 節點名稱。</span><span class="sxs-lookup"><span data-stu-id="3b26e-182">This field represents hello node name used for billing purposes.</span></span> <span data-ttu-id="3b26e-183">使用 toooverride hello 標準偵測的節點。</span><span class="sxs-lookup"><span data-stu-id="3b26e-183">Use it toooverride hello standard detection of nodes.</span></span>

<span data-ttu-id="3b26e-184">最大長度：256</span><span class="sxs-lookup"><span data-stu-id="3b26e-184">Max length: 256</span></span>


## <a name="next-steps"></a><span data-ttu-id="3b26e-185">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3b26e-185">Next steps</span></span>

- <span data-ttu-id="3b26e-186">了解如何太[擴充和篩選遙測](app-insights-api-filtering-sampling.md)。</span><span class="sxs-lookup"><span data-stu-id="3b26e-186">Learn how too[extend and filter telemetry](app-insights-api-filtering-sampling.md).</span></span>
- <span data-ttu-id="3b26e-187">如需 Application Insights 類型和資料模型，請參閱[資料模型](application-insights-data-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3b26e-187">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3b26e-188">請查看標準內容屬性集合[組態](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet)。</span><span class="sxs-lookup"><span data-stu-id="3b26e-188">Check out standard context properties collection [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet).</span></span>
