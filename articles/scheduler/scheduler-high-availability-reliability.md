---
title: "aaaScheduler 高可用性和可靠性"
description: "排程器高可用性和可靠性"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5ec78e60-a9b9-405a-91a8-f010f3872d50
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/16/2016
ms.author: deli
ms.openlocfilehash: 5c9efb333eb42b393adc5deea657ca99206d425e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="231b8-103">排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="231b8-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="231b8-104">Azure 排程器高可用性</span><span class="sxs-lookup"><span data-stu-id="231b8-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="231b8-105">做為 Azure 平台服務的核心，Azure 排程器高度可用，並以地理區域備援服務部署和地理區域複寫為其特色。</span><span class="sxs-lookup"><span data-stu-id="231b8-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="231b8-106">地理區域備援服務部署</span><span class="sxs-lookup"><span data-stu-id="231b8-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="231b8-107">透過 hello 現在是在 Azure 中幾乎每個地理區域中的 UI 使用 azure 排程器。</span><span class="sxs-lookup"><span data-stu-id="231b8-107">Azure Scheduler is available via hello UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="231b8-108">hello Azure 排程器中可用的地區清單為[此處所列](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="231b8-108">hello list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="231b8-109">如果裝載區域中的資料中心呈現無法使用，Azure 排程器的 hello 容錯移轉功能會是，從另一個資料中心 hello 服務可供使用。</span><span class="sxs-lookup"><span data-stu-id="231b8-109">If a data center in a hosted region is rendered unavailable, hello failover capabilities of Azure Scheduler are such that hello service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="231b8-110">地理區域工作複寫</span><span class="sxs-lookup"><span data-stu-id="231b8-110">Geo-regional job replication</span></span>
<span data-ttu-id="231b8-111">不只是 hello Azure 排程器前端可用於管理要求，但您自己的工作也是地理複寫。</span><span class="sxs-lookup"><span data-stu-id="231b8-111">Not only is hello Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="231b8-112">當在一個區域發生中斷時，Azure 排程器容錯移轉，並確保該 hello 執行作業時從另一個資料中心 hello 配對地理區域。</span><span class="sxs-lookup"><span data-stu-id="231b8-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that hello job is run from another data center in hello paired geographic region.</span></span>

<span data-ttu-id="231b8-113">比方說，如果您在美國中南部建立工作，Azure 排程器就會在中北部自動複寫該工作。</span><span class="sxs-lookup"><span data-stu-id="231b8-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="231b8-114">當美國中南部中失敗，則 Azure 排程器可確保從美國中北部執行 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="231b8-114">When there’s a failure in South Central US, Azure Scheduler ensures that hello job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="231b8-115">如此一來，Azure 排程器可確保您的資料會保留在 hello 同一個發生在 Azure 發生錯誤時更廣泛的地理區域。</span><span class="sxs-lookup"><span data-stu-id="231b8-115">As a result, Azure Scheduler ensures that your data stays within hello same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="231b8-116">如此一來，您需要不重複的作業只 tooadd 的高可用性 – Azure 排程器會自動提供高可用性功能，為您的工作。</span><span class="sxs-lookup"><span data-stu-id="231b8-116">As a result, you need not duplicate your job just tooadd high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="231b8-117">Azure 排程器可靠性</span><span class="sxs-lookup"><span data-stu-id="231b8-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="231b8-118">Azure 排程器會保證其本身的高可用性，並採用不同的方法 toouser 建立的工作。</span><span class="sxs-lookup"><span data-stu-id="231b8-118">Azure Scheduler guarantees its own high-availability and takes a different approach toouser-created jobs.</span></span> <span data-ttu-id="231b8-119">例如，您的工作可能會叫用無法使用的 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="231b8-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="231b8-120">Azure 排程器仍會嘗試 tooexecute 您的工作成功，但發生失敗的替代選項 toodeal，提供。</span><span class="sxs-lookup"><span data-stu-id="231b8-120">Azure Scheduler nonetheless tries tooexecute your job successfully, by giving you alternative options toodeal with failure.</span></span> <span data-ttu-id="231b8-121">Azure 排程器會以兩種方式執行此項動作：</span><span class="sxs-lookup"><span data-stu-id="231b8-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="231b8-122">可透過 "retryPolicy" 設定重試原則</span><span class="sxs-lookup"><span data-stu-id="231b8-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="231b8-123">Azure 排程器可讓您 tooconfigure 重試原則。</span><span class="sxs-lookup"><span data-stu-id="231b8-123">Azure Scheduler allows you tooconfigure a retry policy.</span></span> <span data-ttu-id="231b8-124">根據預設，如果工作失敗，排程器會嘗試 hello 作業試四次，30 秒的間隔。</span><span class="sxs-lookup"><span data-stu-id="231b8-124">By default, if a job fails, Scheduler tries hello job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="231b8-125">您可以重新設定此重試原則 toobe 更積極 （例如，十倍，30 秒的間隔） 或更加鬆散 （例如，兩次，每日間隔。）</span><span class="sxs-lookup"><span data-stu-id="231b8-125">You may re-configure this retry policy toobe more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="231b8-126">舉例來說，當這樣做有幫助時，您可能會建立一週執行一次，並叫用 HTTP 端點的工作。</span><span class="sxs-lookup"><span data-stu-id="231b8-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="231b8-127">如果 hello HTTP 端點已關閉的幾個小時執行您的工作時，您可能不想 toowait 一個更多週的 hello 作業 toorun 再次因為即使 hello 預設重試原則將會失敗。</span><span class="sxs-lookup"><span data-stu-id="231b8-127">If hello HTTP endpoint is down for a few hours when your job runs, you may not want toowait one more week for hello job toorun again since even hello default retry policy will fail.</span></span> <span data-ttu-id="231b8-128">在這種情況下，您可能會重新設定 hello 標準重試原則 tooretry 每隔三小時 （舉例來說） 而不是每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="231b8-128">In such cases, you may reconfigure hello standard retry policy tooretry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="231b8-129">如何重試原則，tooconfigure 參照太 toolearn[retryPolicy](scheduler-concepts-terms.md#retrypolicy)。</span><span class="sxs-lookup"><span data-stu-id="231b8-129">toolearn how tooconfigure a retry policy, refer too[retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="231b8-130">可透過 "ErrorAction" 設定替代端點的功能</span><span class="sxs-lookup"><span data-stu-id="231b8-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="231b8-131">如果 Azure 排程器工作的 hello 目標端點仍然無法連線，Azure 排程器會回復 toohello 替代錯誤處理端點後其重試原則。</span><span class="sxs-lookup"><span data-stu-id="231b8-131">If hello target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back toohello alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="231b8-132">如果已設定替代錯誤處理端點，Azure 排程器會叫用它。</span><span class="sxs-lookup"><span data-stu-id="231b8-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="231b8-133">有了替代端點，您自己的工作可用高 hello 字體的失敗。</span><span class="sxs-lookup"><span data-stu-id="231b8-133">With an alternate endpoint, your own jobs are highly available in hello face of failure.</span></span>

<span data-ttu-id="231b8-134">例如，在 hello 圖，Azure 排程器會依照其重試原則 toohit New York web 服務。</span><span class="sxs-lookup"><span data-stu-id="231b8-134">As an example, in hello diagram below, Azure Scheduler follows its retry policy toohit a New York web service.</span></span> <span data-ttu-id="231b8-135">Hello 重試失敗之後，它會檢查是否有替代。</span><span class="sxs-lookup"><span data-stu-id="231b8-135">After hello retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="231b8-136">接著會繼續，並開始進行 toohello 替代 hello 與相同的要求重試原則。</span><span class="sxs-lookup"><span data-stu-id="231b8-136">It then goes ahead and starts making requests toohello alternate with hello same retry policy.</span></span>

![][2]

<span data-ttu-id="231b8-137">請注意，hello 相同的重試原則適用於 tooboth hello 原始動作和 hello 替代錯誤動作。</span><span class="sxs-lookup"><span data-stu-id="231b8-137">Note that hello same retry policy applies tooboth hello original action and hello alternate error action.</span></span> <span data-ttu-id="231b8-138">它也可能 toohave hello 替代錯誤動作的動作類型為 hello 主要動作的動作類型不同。</span><span class="sxs-lookup"><span data-stu-id="231b8-138">It’s also possible toohave hello alternate error action’s action type be different from hello main action’s action type.</span></span> <span data-ttu-id="231b8-139">比方說，hello 主要動作可能會叫用 HTTP 端點，而 hello 錯誤動作而可能儲存體佇列、 服務匯流排佇列或進行錯誤記錄的服務匯流排主題動作。</span><span class="sxs-lookup"><span data-stu-id="231b8-139">For example, while hello main action may be invoking an HTTP endpoint, hello error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="231b8-140">如何 tooconfigure 替代端點，參照太 toolearn[errorAction](scheduler-concepts-terms.md#action-and-erroraction)。</span><span class="sxs-lookup"><span data-stu-id="231b8-140">toolearn how tooconfigure an alternate endpoint, refer too[errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="231b8-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="231b8-141">See Also</span></span>
 [<span data-ttu-id="231b8-142">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="231b8-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="231b8-143">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="231b8-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="231b8-144">開始在 hello Azure 入口網站中使用排程器</span><span class="sxs-lookup"><span data-stu-id="231b8-144">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="231b8-145">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="231b8-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="231b8-146">排程 toobuild 複雜的方式與進階循環使用 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="231b8-146">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="231b8-147">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="231b8-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="231b8-148">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="231b8-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="231b8-149">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="231b8-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="231b8-150">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="231b8-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
