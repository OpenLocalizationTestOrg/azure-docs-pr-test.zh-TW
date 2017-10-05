---
title: "排程器高可用性和可靠性"
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
ms.openlocfilehash: 7e7fe49de7814b6058468d630f8638720e5864f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-high-availability-and-reliability"></a><span data-ttu-id="c9add-103">排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="c9add-103">Scheduler High-Availability and Reliability</span></span>
## <a name="azure-scheduler-high-availability"></a><span data-ttu-id="c9add-104">Azure 排程器高可用性</span><span class="sxs-lookup"><span data-stu-id="c9add-104">Azure Scheduler High-Availability</span></span>
<span data-ttu-id="c9add-105">做為 Azure 平台服務的核心，Azure 排程器高度可用，並以地理區域備援服務部署和地理區域複寫為其特色。</span><span class="sxs-lookup"><span data-stu-id="c9add-105">As a core Azure platform service, Azure Scheduler is highly available and features both geo-redundant service deployment and geo-regional job replication.</span></span>

### <a name="geo-redundant-service-deployment"></a><span data-ttu-id="c9add-106">地理區域備援服務部署</span><span class="sxs-lookup"><span data-stu-id="c9add-106">Geo-redundant service deployment</span></span>
<span data-ttu-id="c9add-107">今日可在 Azure 的幾乎每個地理區域中透過 UI 使用 Azure 排程器。</span><span class="sxs-lookup"><span data-stu-id="c9add-107">Azure Scheduler is available via the UI in almost every geo region that's in Azure today.</span></span> <span data-ttu-id="c9add-108">可以使用 Azure 排程器的區域清單 [列於這裡](https://azure.microsoft.com/regions/#services)。</span><span class="sxs-lookup"><span data-stu-id="c9add-108">The list of regions that Azure Scheduler is available in is [listed here](https://azure.microsoft.com/regions/#services).</span></span> <span data-ttu-id="c9add-109">如果裝載區域中的資料中心表現出無法使用，則 Azure 排程器的容錯移轉功能可從另一個資料中心使用服務。</span><span class="sxs-lookup"><span data-stu-id="c9add-109">If a data center in a hosted region is rendered unavailable, the failover capabilities of Azure Scheduler are such that the service is available from another data center.</span></span>

### <a name="geo-regional-job-replication"></a><span data-ttu-id="c9add-110">地理區域工作複寫</span><span class="sxs-lookup"><span data-stu-id="c9add-110">Geo-regional job replication</span></span>
<span data-ttu-id="c9add-111">Azure 排程器前端不僅可供管理要求使用，您自己的工作也是可以進行地理區域複寫。</span><span class="sxs-lookup"><span data-stu-id="c9add-111">Not only is the Azure Scheduler front-end available for management requests, but your own job is also geo-replicated.</span></span> <span data-ttu-id="c9add-112">在某個區域中斷執行時，Azure 排程器會容錯移轉，並確保從配對的地理區域中的另一個資料中心執行工作。</span><span class="sxs-lookup"><span data-stu-id="c9add-112">When there’s an outage in one region, Azure Scheduler fails over and ensures that the job is run from another data center in the paired geographic region.</span></span>

<span data-ttu-id="c9add-113">比方說，如果您在美國中南部建立工作，Azure 排程器就會在中北部自動複寫該工作。</span><span class="sxs-lookup"><span data-stu-id="c9add-113">For example, if you’ve created a job in South Central US, Azure Scheduler automatically replicates that job in North Central US.</span></span> <span data-ttu-id="c9add-114">在美國中南部失敗時，Azure 排程器會確保工作從美國中北部執行。</span><span class="sxs-lookup"><span data-stu-id="c9add-114">When there’s a failure in South Central US, Azure Scheduler ensures that the job is run from North Central US.</span></span> 

![][1]

<span data-ttu-id="c9add-115">如此一來，Azure 排程器確保如果 Azure 失敗，您的資料會保留在相同的更廣泛地理區域中。</span><span class="sxs-lookup"><span data-stu-id="c9add-115">As a result, Azure Scheduler ensures that your data stays within the same broader geographic region in case of an Azure failure.</span></span> <span data-ttu-id="c9add-116">如此一來，您不需要只為了新增高可用性而重複您的工作 – Azure 排程器會為您的工作自動提供高可用性功能。</span><span class="sxs-lookup"><span data-stu-id="c9add-116">As a result, you need not duplicate your job just to add high availability – Azure Scheduler automatically provides high-availability capabilities for your jobs.</span></span>

## <a name="azure-scheduler-reliability"></a><span data-ttu-id="c9add-117">Azure 排程器可靠性</span><span class="sxs-lookup"><span data-stu-id="c9add-117">Azure Scheduler Reliability</span></span>
<span data-ttu-id="c9add-118">Azure 排程器保證它自己的高可用性，並使用者建立的工作採用不同的方法。</span><span class="sxs-lookup"><span data-stu-id="c9add-118">Azure Scheduler guarantees its own high-availability and takes a different approach to user-created jobs.</span></span> <span data-ttu-id="c9add-119">例如，您的工作可能會叫用無法使用的 HTTP 端點。</span><span class="sxs-lookup"><span data-stu-id="c9add-119">For example, your job may invoke an HTTP endpoint that’s unavailable.</span></span> <span data-ttu-id="c9add-120">Azure 排程器仍會嘗試成功執行您的工作，方法為提供您處理失敗的替代選項。</span><span class="sxs-lookup"><span data-stu-id="c9add-120">Azure Scheduler nonetheless tries to execute your job successfully, by giving you alternative options to deal with failure.</span></span> <span data-ttu-id="c9add-121">Azure 排程器會以兩種方式執行此項動作：</span><span class="sxs-lookup"><span data-stu-id="c9add-121">Azure Scheduler does this in two ways:</span></span>

### <a name="configurable-retry-policy-via-retrypolicy"></a><span data-ttu-id="c9add-122">可透過 "retryPolicy" 設定重試原則</span><span class="sxs-lookup"><span data-stu-id="c9add-122">Configurable Retry Policy via “retryPolicy”</span></span>
<span data-ttu-id="c9add-123">Azure 排程器可讓您設定重試原則。</span><span class="sxs-lookup"><span data-stu-id="c9add-123">Azure Scheduler allows you to configure a retry policy.</span></span> <span data-ttu-id="c9add-124">根據預設，如果工作失敗，排程器會在 30 秒間隔內重新嘗試工作四次。</span><span class="sxs-lookup"><span data-stu-id="c9add-124">By default, if a job fails, Scheduler tries the job again four more times, at 30-second intervals.</span></span> <span data-ttu-id="c9add-125">您可能會將此重試原則重新設定為更積極 (例如，在 30 秒間隔內重試十次) 或鬆散 (例如，每日間隔重複兩次。)</span><span class="sxs-lookup"><span data-stu-id="c9add-125">You may re-configure this retry policy to be more aggressive (for example, ten times, at 30-second intervals) or looser (for example, two times, at daily intervals.)</span></span>

<span data-ttu-id="c9add-126">舉例來說，當這樣做有幫助時，您可能會建立一週執行一次，並叫用 HTTP 端點的工作。</span><span class="sxs-lookup"><span data-stu-id="c9add-126">As an example of when this may help, you may create a job that runs once a week and invokes an HTTP endpoint.</span></span> <span data-ttu-id="c9add-127">當您的工作執行時，如果 HTTP 端點已關閉幾個小時，則您可能不想多等待一週，讓工作重新執行，即使預設重試原則失敗也一樣。</span><span class="sxs-lookup"><span data-stu-id="c9add-127">If the HTTP endpoint is down for a few hours when your job runs, you may not want to wait one more week for the job to run again since even the default retry policy will fail.</span></span> <span data-ttu-id="c9add-128">在這種情況下，您可能會每隔三個小時 (舉例來說) 重新設定要重試的標準重試原則，而不是每隔 30 秒。</span><span class="sxs-lookup"><span data-stu-id="c9add-128">In such cases, you may reconfigure the standard retry policy to retry every three hours (for example) instead of every 30 seconds.</span></span>

<span data-ttu-id="c9add-129">若要了解如何設定重試原則，請參閱 [retryPolicy](scheduler-concepts-terms.md#retrypolicy)。</span><span class="sxs-lookup"><span data-stu-id="c9add-129">To learn how to configure a retry policy, refer to [retryPolicy](scheduler-concepts-terms.md#retrypolicy).</span></span>

### <a name="alternate-endpoint-configurability-via-erroraction"></a><span data-ttu-id="c9add-130">可透過 "ErrorAction" 設定替代端點的功能</span><span class="sxs-lookup"><span data-stu-id="c9add-130">Alternate Endpoint Configurability via “errorAction”</span></span>
<span data-ttu-id="c9add-131">如果您的 Azure 排程器工作的目標端點仍然無法連線，Azure 排程器會在遵循其重試原則之後回復到替代錯誤處理端點。</span><span class="sxs-lookup"><span data-stu-id="c9add-131">If the target endpoint for your Azure Scheduler job remains unreachable, Azure Scheduler falls back to the alternate error-handling endpoint after following its retry policy.</span></span> <span data-ttu-id="c9add-132">如果已設定替代錯誤處理端點，Azure 排程器會叫用它。</span><span class="sxs-lookup"><span data-stu-id="c9add-132">If an alternate error-handling endpoint is configured, Azure Scheduler invokes it.</span></span> <span data-ttu-id="c9add-133">有了替代端點，可在面臨失敗時，高度使用您自己的工作。</span><span class="sxs-lookup"><span data-stu-id="c9add-133">With an alternate endpoint, your own jobs are highly available in the face of failure.</span></span>

<span data-ttu-id="c9add-134">舉例來說，在下圖中，Azure 排程器會遵循其重試原則，點閱紐約 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="c9add-134">As an example, in the diagram below, Azure Scheduler follows its retry policy to hit a New York web service.</span></span> <span data-ttu-id="c9add-135">重試失敗之後，它會檢查是否有替代項。</span><span class="sxs-lookup"><span data-stu-id="c9add-135">After the retries fail, it checks if there's an alternate.</span></span> <span data-ttu-id="c9add-136">接著會繼續進行，並開始對使用相同重試原則的替代項提出要求。</span><span class="sxs-lookup"><span data-stu-id="c9add-136">It then goes ahead and starts making requests to the alternate with the same retry policy.</span></span>

![][2]

<span data-ttu-id="c9add-137">請注意，相同的重試原則同時適用於原始動作和替代錯誤動作。</span><span class="sxs-lookup"><span data-stu-id="c9add-137">Note that the same retry policy applies to both the original action and the alternate error action.</span></span> <span data-ttu-id="c9add-138">此外，替代錯誤動作的動作類型也可能與主要動作的動作類型不同。</span><span class="sxs-lookup"><span data-stu-id="c9add-138">It’s also possible to have the alternate error action’s action type be different from the main action’s action type.</span></span> <span data-ttu-id="c9add-139">例如，當主要動作可能叫用 HTTP 端點時，而錯誤動作則可能改為進行錯誤記錄的儲存體佇列、服務匯流排佇列或服務匯流排主題動作。</span><span class="sxs-lookup"><span data-stu-id="c9add-139">For example, while the main action may be invoking an HTTP endpoint, the error action may instead be a storage queue, service bus queue, or service bus topic action that does error-logging.</span></span>

<span data-ttu-id="c9add-140">若要了解如何設定替代端點，請參閱 [errorAction](scheduler-concepts-terms.md#action-and-erroraction)。</span><span class="sxs-lookup"><span data-stu-id="c9add-140">To learn how to configure an alternate endpoint, refer to [errorAction](scheduler-concepts-terms.md#action-and-erroraction).</span></span>

## <a name="see-also"></a><span data-ttu-id="c9add-141">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c9add-141">See Also</span></span>
 [<span data-ttu-id="c9add-142">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="c9add-142">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="c9add-143">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="c9add-143">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="c9add-144">在 Azure 入口網站中開始使用排程器</span><span class="sxs-lookup"><span data-stu-id="c9add-144">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="c9add-145">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="c9add-145">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="c9add-146">如何使用 Azure 排程器建立複雜的排程和進階週期</span><span class="sxs-lookup"><span data-stu-id="c9add-146">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="c9add-147">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="c9add-147">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="c9add-148">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="c9add-148">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="c9add-149">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="c9add-149">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="c9add-150">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="c9add-150">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

[1]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image1.png

[2]: ./media/scheduler-high-availability-reliability/scheduler-high-availability-reliability-image2.png
