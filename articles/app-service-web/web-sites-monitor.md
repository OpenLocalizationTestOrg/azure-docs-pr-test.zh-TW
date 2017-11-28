---
title: "aaaMonitor Azure App Service 中的應用程式 |Microsoft 文件"
description: "了解如何使用 Azure App Service 中的 toomonitor 應用程式 hello Azure 入口網站。"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: d273da4e-07de-48e0-b99d-4020d84a425e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2016
ms.author: byvinyal
ms.openlocfilehash: 80d5a466102a894a49d04ae35aa54cc1d05a58df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-monitor-apps-in-azure-app-service"></a><span data-ttu-id="3aa04-103">作法：監視 Azure App Service 中的應用程式</span><span class="sxs-lookup"><span data-stu-id="3aa04-103">How to: Monitor Apps in Azure App Service</span></span>
<span data-ttu-id="3aa04-104">[應用程式服務](http://go.microsoft.com/fwlink/?LinkId=529714)會提供內建的監視功能，在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3aa04-104">[App Service](http://go.microsoft.com/fwlink/?LinkId=529714) provides built in monitoring functionality in hello [Azure Portal](https://portal.azure.com).</span></span>
<span data-ttu-id="3aa04-105">這包括 hello 能力 tooreview**配額**和**度量**應用程式，以及設定的 App Service 方案 hello**警示**，甚至**調整**自動根據這些度量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-105">This includes hello ability tooreview **quotas** and **metrics** for an app as well as hello App Service plan, setting up **alerts** and even **scaling** automatically based on these metrics.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="understanding-quotas-and-metrics"></a><span data-ttu-id="3aa04-106">了解配額和計量</span><span class="sxs-lookup"><span data-stu-id="3aa04-106">Understanding Quotas and Metrics</span></span>
### <a name="quotas"></a><span data-ttu-id="3aa04-107">配額</span><span class="sxs-lookup"><span data-stu-id="3aa04-107">Quotas</span></span>
<span data-ttu-id="3aa04-108">App Service 中裝載的應用程式是主體 toocertain*限制*上可以使用的資源。</span><span class="sxs-lookup"><span data-stu-id="3aa04-108">Applications hosted in App Service are subject toocertain *limits* on the resources they can use.</span></span> <span data-ttu-id="3aa04-109">hello 限制由定義 hello **App Service 方案**hello 應用程式相關聯。</span><span class="sxs-lookup"><span data-stu-id="3aa04-109">hello limits are defined by hello **App Service plan** associated with hello app.</span></span>

<span data-ttu-id="3aa04-110">如果 hello 應用程式裝載在**免費**或**共用**計劃，則會由 hello hello hello 應用程式可以使用的資源限制**配額**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-110">If hello application is hosted in a **Free** or **Shared** plan, then hello limits on hello resources hello app can use are defined by **Quotas**.</span></span>

<span data-ttu-id="3aa04-111">如果 hello 應用程式裝載在**基本**，**標準**或**Premium**計劃，然後由 hello 設定 hello 他們可以使用的資源上的 hello 限制**大小**（小型、 中型的大） 和**執行個體計數**（1、 2、 3 …） 的 hello **App Service 方案**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-111">If hello application is hosted in a **Basic**, **Standard** or **Premium** plan, then hello limits on hello resources they can use are set by hello **size** (Small, Medium, Large) and **instance count** (1, 2, 3, ...) of hello **App Service plan**.</span></span>

<span data-ttu-id="3aa04-112">**免費**或**共用**應用程式的**配額**如下︰</span><span class="sxs-lookup"><span data-stu-id="3aa04-112">**Quotas** for **Free** or **Shared** apps are:</span></span>

* <span data-ttu-id="3aa04-113">**CPU (短期)**</span><span class="sxs-lookup"><span data-stu-id="3aa04-113">**CPU(Short)**</span></span>
  * <span data-ttu-id="3aa04-114">此應用程式在 5 分鐘間隔內允許的 CPU 數量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-114">Amount of CPU allowed for this application in a 5-minute interval.</span></span> <span data-ttu-id="3aa04-115">此配額會每 5 分鐘重設一次。</span><span class="sxs-lookup"><span data-stu-id="3aa04-115">This quota re-sets every 5 minutes.</span></span>
* <span data-ttu-id="3aa04-116">**CPU (天)**</span><span class="sxs-lookup"><span data-stu-id="3aa04-116">**CPU(Day)**</span></span>
  * <span data-ttu-id="3aa04-117">此應用程式在 1 天內允許的 CPU 總量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-117">Total amount of CPU allowed for this application in a day.</span></span> <span data-ttu-id="3aa04-118">此配額會每隔 24 小時在午夜 (UTC) 重設一次。</span><span class="sxs-lookup"><span data-stu-id="3aa04-118">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="3aa04-119">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="3aa04-119">**Memory**</span></span>
  * <span data-ttu-id="3aa04-120">此應用程式允許的記憶體總量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-120">Total amount of memory allowed for this application.</span></span>
* <span data-ttu-id="3aa04-121">**頻寬**</span><span class="sxs-lookup"><span data-stu-id="3aa04-121">**Bandwidth**</span></span>
  * <span data-ttu-id="3aa04-122">此應用程式在 1 天內允許的連出頻寬總量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-122">Total amount of outgoing bandwidth allowed for this application in a day.</span></span>
    <span data-ttu-id="3aa04-123">此配額會每隔 24 小時在午夜 (UTC) 重設一次。</span><span class="sxs-lookup"><span data-stu-id="3aa04-123">This quota re-sets every 24 hours at midnight UTC.</span></span>
* <span data-ttu-id="3aa04-124">**Filesystem**</span><span class="sxs-lookup"><span data-stu-id="3aa04-124">**Filesystem**</span></span>
  * <span data-ttu-id="3aa04-125">允許的儲存體總量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-125">Total amount of storage allowed.</span></span>

<span data-ttu-id="3aa04-126">hello 只配額適用 tooapps 裝載於**基本**，**標準**和**Premium**計劃是**Filesystem**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-126">hello only quota applicable tooapps hosted on **Basic**, **Standard** and **Premium** plans is **Filesystem**.</span></span>

<span data-ttu-id="3aa04-127">Hello 特定配額、 限制和 hello 不同的應用程式服務 Sku 的可用功能的詳細資訊可以在這裡找到： [Azure 訂用帳戶服務限制](../azure-subscription-service-limits.md#app-service-limits)</span><span class="sxs-lookup"><span data-stu-id="3aa04-127">More information about hello specific quotas, limits and features available to hello different App Service SKUs can be found here: [Azure Subscription Service Limits](../azure-subscription-service-limits.md#app-service-limits)</span></span>

#### <a name="quota-enforcement"></a><span data-ttu-id="3aa04-128">強制配額</span><span class="sxs-lookup"><span data-stu-id="3aa04-128">Quota Enforcement</span></span>
<span data-ttu-id="3aa04-129">如果其使用方式中的應用程式超過 hello **CPU （短整數）**， **CPU （天）**，或**頻寬**配額則 hello 應用程式將會停止，直到 hello 配額重新設定。</span><span class="sxs-lookup"><span data-stu-id="3aa04-129">If an application in its usage exceeds hello **CPU (short)**, **CPU (Day)**, or **bandwidth** quota then hello application will be stopped until hello quota re-sets.</span></span> <span data-ttu-id="3aa04-130">在此期間，所有連入要求都會導致 **HTTP 403**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-130">During this time, all incoming requests will result in an **HTTP 403**.</span></span>
![][http403]

<span data-ttu-id="3aa04-131">如果應用程式的 hello**記憶體**超過配額時，則 hello 應用程式會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="3aa04-131">If hello application **memory** quota is exceeded, then hello application will be re-started.</span></span>

<span data-ttu-id="3aa04-132">如果 hello **Filesystem**超過配額時，則任何寫入作業將會失敗，這包括寫入 toologs。</span><span class="sxs-lookup"><span data-stu-id="3aa04-132">If hello **Filesystem** quota is exceeded, then any write operation will fail, this includes writing toologs.</span></span>

<span data-ttu-id="3aa04-133">升級您的 App Service 方案，即可在應用程式中增加或移除配額。</span><span class="sxs-lookup"><span data-stu-id="3aa04-133">Quotas can be increased or removed from your app by upgrading your App Service plan.</span></span>

### <a name="metrics"></a><span data-ttu-id="3aa04-134">度量</span><span class="sxs-lookup"><span data-stu-id="3aa04-134">Metrics</span></span>
<span data-ttu-id="3aa04-135">**度量**提供 hello 應用程式或應用程式服務方案行為的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3aa04-135">**Metrics** provide information about hello app, or App Service plan's behavior.</span></span>

<span data-ttu-id="3aa04-136">如**應用程式**，hello 可用度量：</span><span class="sxs-lookup"><span data-stu-id="3aa04-136">For an **Application**, hello available metrics are:</span></span>

* <span data-ttu-id="3aa04-137">**平均回應時間**</span><span class="sxs-lookup"><span data-stu-id="3aa04-137">**Average Response Time**</span></span>
  * <span data-ttu-id="3aa04-138">hello 毫秒 hello 應用程式 tooserve 要求所花費的平均時間。</span><span class="sxs-lookup"><span data-stu-id="3aa04-138">hello average time taken for hello app tooserve requests in ms.</span></span>
* <span data-ttu-id="3aa04-139">**平均記憶體工作集**</span><span class="sxs-lookup"><span data-stu-id="3aa04-139">**Average memory working set**</span></span>
  * <span data-ttu-id="3aa04-140">hello 平均量中 Mib hello 應用程式所使用的記憶體。</span><span class="sxs-lookup"><span data-stu-id="3aa04-140">hello average amount of memory in MiBs used by hello app.</span></span>
* <span data-ttu-id="3aa04-141">**CPU 時間**</span><span class="sxs-lookup"><span data-stu-id="3aa04-141">**CPU Time**</span></span>
  * <span data-ttu-id="3aa04-142">hello CPU 數量 hello 應用程式所耗用的秒數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-142">hello amount of CPU in seconds consumed by hello app.</span></span> <span data-ttu-id="3aa04-143">如需此計量的詳細資訊，請參閱︰[CPU 時間與 CPU 百分比](#cpu-time-vs-cpu-percentage)</span><span class="sxs-lookup"><span data-stu-id="3aa04-143">For more information about this metric see: [CPU time vs CPU percentage](#cpu-time-vs-cpu-percentage)</span></span>
* <span data-ttu-id="3aa04-144">**資料輸入**</span><span class="sxs-lookup"><span data-stu-id="3aa04-144">**Data In**</span></span>
  * <span data-ttu-id="3aa04-145">hello hello Mib 中的應用程式所使用的連入頻寬量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-145">hello amount of incoming bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="3aa04-146">**資料輸出**</span><span class="sxs-lookup"><span data-stu-id="3aa04-146">**Data Out**</span></span>
  * <span data-ttu-id="3aa04-147">hello hello Mib 中的應用程式所使用的連出頻寬量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-147">hello amount of outgoing bandwidth consumed by hello app in MiBs.</span></span>
* <span data-ttu-id="3aa04-148">**Http 2xx**</span><span class="sxs-lookup"><span data-stu-id="3aa04-148">**Http 2xx**</span></span>
  * <span data-ttu-id="3aa04-149">導致 http 狀態碼 >= 200 但 < 300 的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-149">Count of requests resulting in a http status code >= 200 but < 300.</span></span>
* <span data-ttu-id="3aa04-150">**Http 3xx**</span><span class="sxs-lookup"><span data-stu-id="3aa04-150">**Http 3xx**</span></span>
  * <span data-ttu-id="3aa04-151">導致 http 狀態碼 >= 300 但 < 400 的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-151">Count of requests resulting in a http status code >= 300 but < 400.</span></span>
* <span data-ttu-id="3aa04-152">**Http 401**</span><span class="sxs-lookup"><span data-stu-id="3aa04-152">**Http 401**</span></span>
  * <span data-ttu-id="3aa04-153">導致 HTTP 401 狀態碼的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-153">Count of requests resulting in HTTP 401 status code.</span></span>
* <span data-ttu-id="3aa04-154">**Http 403**</span><span class="sxs-lookup"><span data-stu-id="3aa04-154">**Http 403**</span></span>
  * <span data-ttu-id="3aa04-155">導致 HTTP 403 狀態碼的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-155">Count of requests resulting in HTTP 403 status code.</span></span>
* <span data-ttu-id="3aa04-156">**Http 404**</span><span class="sxs-lookup"><span data-stu-id="3aa04-156">**Http 404**</span></span>
  * <span data-ttu-id="3aa04-157">導致 HTTP 404 狀態碼的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-157">Count of requests resulting in HTTP 404 status code.</span></span>
* <span data-ttu-id="3aa04-158">**Http 406**</span><span class="sxs-lookup"><span data-stu-id="3aa04-158">**Http 406**</span></span>
  * <span data-ttu-id="3aa04-159">導致 HTTP 406 狀態碼的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-159">Count of requests resulting in HTTP 406 status code.</span></span>
* <span data-ttu-id="3aa04-160">**Http 4xx**</span><span class="sxs-lookup"><span data-stu-id="3aa04-160">**Http 4xx**</span></span>
  * <span data-ttu-id="3aa04-161">導致 http 狀態碼 >= 400 但 < 500 的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-161">Count of requests resulting in a http status code >= 400 but < 500.</span></span>
* <span data-ttu-id="3aa04-162">**Http 伺服器錯誤**</span><span class="sxs-lookup"><span data-stu-id="3aa04-162">**Http Server Errors**</span></span>
  * <span data-ttu-id="3aa04-163">導致 http 狀態碼 >= 500 但 < 600 的要求計數。</span><span class="sxs-lookup"><span data-stu-id="3aa04-163">Count of requests resulting in a http status code >= 500 but < 600.</span></span>
* <span data-ttu-id="3aa04-164">**記憶體工作集**</span><span class="sxs-lookup"><span data-stu-id="3aa04-164">**Memory working set**</span></span>
  * <span data-ttu-id="3aa04-165">目前的 Mib 中的 hello 應用程式所使用的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-165">Current amount of memory used by hello app in MiBs.</span></span>
* <span data-ttu-id="3aa04-166">**要求**</span><span class="sxs-lookup"><span data-stu-id="3aa04-166">**Requests**</span></span>
  * <span data-ttu-id="3aa04-167">要求總數 (不論其導致的 HTTP 狀態碼為何)。</span><span class="sxs-lookup"><span data-stu-id="3aa04-167">Total number of requests regardless of their resulting HTTP status code.</span></span>

<span data-ttu-id="3aa04-168">如**App Service 方案**，hello 可用度量：</span><span class="sxs-lookup"><span data-stu-id="3aa04-168">For an **App Service plan**, hello available metrics are:</span></span>

> [!NOTE]
> <span data-ttu-id="3aa04-169">App Service 方案計量只適用於**基本**、**標準**和**進階** SKU 中的方案。</span><span class="sxs-lookup"><span data-stu-id="3aa04-169">App Service plan metrics are only available for plans in **Basic**, **Standard** and **Premium** SKU.</span></span>
> 
> 

* <span data-ttu-id="3aa04-170">**CPU 百分比**</span><span class="sxs-lookup"><span data-stu-id="3aa04-170">**CPU Percentage**</span></span>
  * <span data-ttu-id="3aa04-171">hello 平均 CPU 使用 hello 計劃的所有執行個體。</span><span class="sxs-lookup"><span data-stu-id="3aa04-171">hello average CPU used across all instances of hello plan.</span></span>
* <span data-ttu-id="3aa04-172">**記憶體百分比**</span><span class="sxs-lookup"><span data-stu-id="3aa04-172">**Memory Percentage**</span></span>
  * <span data-ttu-id="3aa04-173">hello hello 計劃的所有執行個體之間使用的平均的記憶體。</span><span class="sxs-lookup"><span data-stu-id="3aa04-173">hello average memory used across all instances of hello plan.</span></span>
* <span data-ttu-id="3aa04-174">**資料輸入**</span><span class="sxs-lookup"><span data-stu-id="3aa04-174">**Data In**</span></span>
  * <span data-ttu-id="3aa04-175">hello 平均跨 hello 計劃的所有執行個體使用的連入頻寬。</span><span class="sxs-lookup"><span data-stu-id="3aa04-175">hello average incoming bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="3aa04-176">**資料輸出**</span><span class="sxs-lookup"><span data-stu-id="3aa04-176">**Data Out**</span></span>
  * <span data-ttu-id="3aa04-177">hello 平均傳出 hello 計劃的所有執行個體所使用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="3aa04-177">hello average outgoing bandwidth used across all instances of hello plan.</span></span>
* <span data-ttu-id="3aa04-178">**磁碟佇列長度**</span><span class="sxs-lookup"><span data-stu-id="3aa04-178">**Disk Queue Length**</span></span>
  * <span data-ttu-id="3aa04-179">hello 平均數的讀取和寫入要求排入佇列的儲存體上。</span><span class="sxs-lookup"><span data-stu-id="3aa04-179">hello average number of both read and write requests that were queued on storage.</span></span> <span data-ttu-id="3aa04-180">高磁碟佇列長度是可能會變慢，因為 tooexcessive 磁碟 I/O 的應用程式的指示。</span><span class="sxs-lookup"><span data-stu-id="3aa04-180">A high disk queue length is an indication of an application that might be slowing down due tooexcessive disk I/O.</span></span>
* <span data-ttu-id="3aa04-181">**Http 佇列長度**</span><span class="sxs-lookup"><span data-stu-id="3aa04-181">**Http Queue Length**</span></span>
  * <span data-ttu-id="3aa04-182">hello 的以前 toosit hello 佇列執行的 HTTP 要求的平均數目。</span><span class="sxs-lookup"><span data-stu-id="3aa04-182">hello average number of HTTP requests that had toosit on hello queue before being fulfilled.</span></span> <span data-ttu-id="3aa04-183">HTTP 佇列長度很大或不斷增加是方案負載過重的徵兆。</span><span class="sxs-lookup"><span data-stu-id="3aa04-183">A high or increasing HTTP Queue length is a symptom of a plan under heavy load.</span></span>

### <a name="cpu-time-vs-cpu-percentage"></a><span data-ttu-id="3aa04-184">CPU 時間與 CPU 百分比</span><span class="sxs-lookup"><span data-stu-id="3aa04-184">CPU time vs CPU percentage</span></span>
<!-- toodo: Fix Anchor (#CPU-time-vs.-CPU-percentage) -->

<span data-ttu-id="3aa04-185">有 2 個計量可反映 CPU 使用量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-185">There are 2 metrics that reflect CPU usage.</span></span> <span data-ttu-id="3aa04-186">**CPU 時間**與 **CPU 百分比**</span><span class="sxs-lookup"><span data-stu-id="3aa04-186">**CPU time** and **CPU percentage**</span></span>

<span data-ttu-id="3aa04-187">**CPU 時間**很有用的應用程式裝載於**免費**或**共用**計劃，因為其配額的其中一個定義在 hello 應用程式所使用的 CPU 分鐘。</span><span class="sxs-lookup"><span data-stu-id="3aa04-187">**CPU Time** is useful for apps hosted in **Free** or **Shared** plans since one of their quotas is defined in CPU minutes used by hello app.</span></span>

<span data-ttu-id="3aa04-188">**CPU 百分比**上 hello 另一方面是有用的應用程式裝載於**基本**，**標準**和**premium**計劃，因為它們可以向外延展和此標準就代表 hello 的所有執行個體的整體使用狀況。</span><span class="sxs-lookup"><span data-stu-id="3aa04-188">**CPU percentage** on hello other hand is useful for apps hosted in **basic**, **standard** and **premium** plans since they can be scaled out and this metric is a good indication of hello overall usage across all instances.</span></span>

## <a name="metrics-granularity-and-retention-policy"></a><span data-ttu-id="3aa04-189">計量資料粒度和保留原則</span><span class="sxs-lookup"><span data-stu-id="3aa04-189">Metrics Granularity and Retention Policy</span></span>
<span data-ttu-id="3aa04-190">記錄和彙總以 hello hello 服務應用程式和應用程式服務方案的度量資料粒度和保留原則：</span><span class="sxs-lookup"><span data-stu-id="3aa04-190">Metrics for an application and app service plan are logged and aggregated by hello service with hello following granularities and retention policies:</span></span>

* <span data-ttu-id="3aa04-191">**分鐘**資料粒度度量會保留 **48 小時**</span><span class="sxs-lookup"><span data-stu-id="3aa04-191">**Minute** granularity metrics are retained for **48 hours**</span></span>
* <span data-ttu-id="3aa04-192">**小時**資料粒度度量會保留 **30 天**</span><span class="sxs-lookup"><span data-stu-id="3aa04-192">**Hour** granularity metrics are retained for **30 days**</span></span>
* <span data-ttu-id="3aa04-193">**天**資料粒度度量會保留 **90 天**</span><span class="sxs-lookup"><span data-stu-id="3aa04-193">**Day** granularity metrics are retained for **90 days**</span></span>

## <a name="monitoring-quotas-and-metrics-in-hello-azure-portal"></a><span data-ttu-id="3aa04-194">Hello Azure 入口網站中的監視配額和計量。</span><span class="sxs-lookup"><span data-stu-id="3aa04-194">Monitoring Quotas and Metrics in hello Azure Portal.</span></span>
<span data-ttu-id="3aa04-195">您可以檢閱 hello hello 不同狀態**配額**和**度量**影響的應用程式在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="3aa04-195">You can review hello status of hello different **quotas** and **metrics** affecting an application in hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="3aa04-196">在 [設定] > **配額** 之下可以找到 ![][quotas]
**配額**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-196">![][quotas]
**Quotas** can be found under Settings>**Quotas**.</span></span> <span data-ttu-id="3aa04-197">hello UX 可讓您檢閱: （1) hello 配額名稱、 （2） 重設的間隔、 （3） 其目前的限制和 （4） 目前的值。</span><span class="sxs-lookup"><span data-stu-id="3aa04-197">hello UX allows you to review: (1) hello quotas name, (2) its reset interval, (3) its current limit and (4) current value.</span></span>

<span data-ttu-id="3aa04-198">![][metrics]
**度量**可以直接從 hello 資源刀鋒視窗存取。</span><span class="sxs-lookup"><span data-stu-id="3aa04-198">![][metrics]
**Metrics** can be access directly from hello resource blade.</span></span> <span data-ttu-id="3aa04-199">您也可以自訂的 hello 圖表: （1)**按一下**它，然後選取 (2)**編輯圖表**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-199">You can also customize hello chart by: (1) **click** on it, and select (2) **edit chart**.</span></span>
<span data-ttu-id="3aa04-200">從這裡您可以變更 hello (3)**時間範圍**、 (4)**圖表類型**，和 (5)**度量**toodisplay。</span><span class="sxs-lookup"><span data-stu-id="3aa04-200">From here you can change hello (3) **time range**, (4) **chart type**, and (5) **metrics** toodisplay.</span></span>  

<span data-ttu-id="3aa04-201">您可以在此進一步了解計量︰[監視服務計量](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md)。</span><span class="sxs-lookup"><span data-stu-id="3aa04-201">You can learn more about metrics here: [Monitor service metrics](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

## <a name="alerts-and-autoscale"></a><span data-ttu-id="3aa04-202">警示和自動調整</span><span class="sxs-lookup"><span data-stu-id="3aa04-202">Alerts and Autoscale</span></span>
<span data-ttu-id="3aa04-203">度量的應用程式或應用程式服務計劃可以接到 tooalerts，toolearn 程式的詳細資訊，請參閱[接收警示通知](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="3aa04-203">Metrics for an App or App Service plan can be hooked up tooalerts, toolearn more about this, see [Receive alert notifications](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)</span></span>

<span data-ttu-id="3aa04-204">基本、標準或進階 App Service 方案中裝載的 App Service 應用程式支援 **自動調整**。</span><span class="sxs-lookup"><span data-stu-id="3aa04-204">App Service apps hosted in basic, standard or premium App Service Plans support **autoscale**.</span></span> <span data-ttu-id="3aa04-205">這可讓您監視 App Service 方案計量，可以增加或減少 hello 視需要提供其他資源的執行個體計數的 tooconfigure 規則或儲存 money hello 應用程式時過度佈建。</span><span class="sxs-lookup"><span data-stu-id="3aa04-205">This allows you tooconfigure rules that monitor the App Service plan metrics and can increase or decrease hello instance count providing additional resources as needed, or saving money when hello application is over-provision.</span></span> <span data-ttu-id="3aa04-206">您可以進一步了解自動調整規模：[如何 tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md)和這裡[Azure 監視的自動調整的最佳做法](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span><span class="sxs-lookup"><span data-stu-id="3aa04-206">You can learn more about auto scale here: [How tooScale](../monitoring-and-diagnostics/insights-how-to-scale.md) and here [Best practices for Azure Monitor autoscaling](../monitoring-and-diagnostics/insights-autoscale-best-practices.md)</span></span>

> [!NOTE]
> <span data-ttu-id="3aa04-207">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="3aa04-207">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3aa04-208">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="3aa04-208">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="3aa04-209">變更的項目</span><span class="sxs-lookup"><span data-stu-id="3aa04-209">What's changed</span></span>
* <span data-ttu-id="3aa04-210">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3aa04-210">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[fzilla]:http://go.microsoft.com/fwlink/?LinkId=247914
[vmsizes]:http://go.microsoft.com/fwlink/?LinkID=309169



<!-- Images. -->
[http403]: ./media/web-sites-monitor/http403.png
[quotas]: ./media/web-sites-monitor/quotas.png
[metrics]: ./media/web-sites-monitor/metrics.png
