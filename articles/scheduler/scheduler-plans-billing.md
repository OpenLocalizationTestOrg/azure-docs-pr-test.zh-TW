---
title: "Azure 排程器的計劃和計費"
description: "Azure 排程器的計劃和計費"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 13a2be8c-dc14-46cc-ab7d-5075bfd4d724
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: f0662230c5d1663e37ee2be58f234934ec3d55dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="plans-and-billing-in-azure-scheduler"></a><span data-ttu-id="b6210-103">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="b6210-103">Plans and Billing in Azure Scheduler</span></span>
## <a name="job-collection-plans"></a><span data-ttu-id="b6210-104">工作集合計劃</span><span class="sxs-lookup"><span data-stu-id="b6210-104">Job Collection Plans</span></span>
<span data-ttu-id="b6210-105">工作集合是 Azure 排程器中可計費的實體。</span><span class="sxs-lookup"><span data-stu-id="b6210-105">Job collections are the billable entity in Azure Scheduler.</span></span> <span data-ttu-id="b6210-106">工作集合包含許多工作，並分成三個計劃 (免費、標準和高階)，如下所述。</span><span class="sxs-lookup"><span data-stu-id="b6210-106">Job collections contain a number of jobs and come in three plans – Free, Standard, and Premium – that are described below.</span></span>

| <span data-ttu-id="b6210-107">**工作集合計劃**</span><span class="sxs-lookup"><span data-stu-id="b6210-107">**Job Collection Plan**</span></span> | <span data-ttu-id="b6210-108">**每個工作集合的工作數上限**</span><span class="sxs-lookup"><span data-stu-id="b6210-108">**Max # of Jobs per Job Collection**</span></span> | <span data-ttu-id="b6210-109">**最大週期**</span><span class="sxs-lookup"><span data-stu-id="b6210-109">**Max Recurrence**</span></span> | <span data-ttu-id="b6210-110">**每個訂用帳戶的工作集合數上限**</span><span class="sxs-lookup"><span data-stu-id="b6210-110">**Max Job Collections per Subscription**</span></span> | <span data-ttu-id="b6210-111">**限制**</span><span class="sxs-lookup"><span data-stu-id="b6210-111">**Limits**</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="b6210-112">**免費**</span><span class="sxs-lookup"><span data-stu-id="b6210-112">**Free**</span></span> |<span data-ttu-id="b6210-113">每個工作集合 5 個工作</span><span class="sxs-lookup"><span data-stu-id="b6210-113">5 jobs per job collection</span></span> |<span data-ttu-id="b6210-114">每小時一次。</span><span class="sxs-lookup"><span data-stu-id="b6210-114">Once per hour.</span></span> <span data-ttu-id="b6210-115">執行工作不得超過一個小時</span><span class="sxs-lookup"><span data-stu-id="b6210-115">Cannot execute jobs more often than once an hour</span></span> |<span data-ttu-id="b6210-116">一個訂用帳戶最多允許 1 個免費工作集合</span><span class="sxs-lookup"><span data-stu-id="b6210-116">A subscription is allowed up to 1 free job collection</span></span> |<span data-ttu-id="b6210-117">無法使用 [HTTP 輸出授權物件](scheduler-outbound-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b6210-117">Cannot use [HTTP outbound authorization object](scheduler-outbound-authentication.md)</span></span> |
| <span data-ttu-id="b6210-118">**標準**</span><span class="sxs-lookup"><span data-stu-id="b6210-118">**Standard**</span></span> |<span data-ttu-id="b6210-119">每個工作集合 50 個工作</span><span class="sxs-lookup"><span data-stu-id="b6210-119">50 jobs per job collection</span></span> |<span data-ttu-id="b6210-120">每分鐘一次。</span><span class="sxs-lookup"><span data-stu-id="b6210-120">Once per minute.</span></span> <span data-ttu-id="b6210-121">執行工作不得超過一分鐘</span><span class="sxs-lookup"><span data-stu-id="b6210-121">Cannot execute jobs more often than once a minute</span></span> |<span data-ttu-id="b6210-122">一個訂用帳戶允許最多 100 個標準工作集合</span><span class="sxs-lookup"><span data-stu-id="b6210-122">A subscription is allowed up to 100 standard job collections</span></span> |<span data-ttu-id="b6210-123">存取排程器的完整功能集</span><span class="sxs-lookup"><span data-stu-id="b6210-123">Access to full feature set of Scheduler</span></span> |
| <span data-ttu-id="b6210-124">**P10 Premium**</span><span class="sxs-lookup"><span data-stu-id="b6210-124">**P10 Premium**</span></span> |<span data-ttu-id="b6210-125">每個工作集合 50 個工作</span><span class="sxs-lookup"><span data-stu-id="b6210-125">50 jobs per job collection</span></span> |<span data-ttu-id="b6210-126">每分鐘一次。</span><span class="sxs-lookup"><span data-stu-id="b6210-126">Once per minute.</span></span> <span data-ttu-id="b6210-127">執行工作不得超過一分鐘</span><span class="sxs-lookup"><span data-stu-id="b6210-127">Cannot execute jobs more often than once a minute</span></span> |<span data-ttu-id="b6210-128">一個訂用帳戶允許最多 10,000 個 P10 進階工作集合。</span><span class="sxs-lookup"><span data-stu-id="b6210-128">A subscription is allowed up to 10,000 P10 Premium job collections.</span></span> <span data-ttu-id="b6210-129">如需詳細資訊，請<a href="mailto:wapteams@microsoft.com">與我們連絡</a>。</span><span class="sxs-lookup"><span data-stu-id="b6210-129"><a href="mailto:wapteams@microsoft.com">Contact us</a> for more.</span></span> |<span data-ttu-id="b6210-130">存取排程器的完整功能集</span><span class="sxs-lookup"><span data-stu-id="b6210-130">Access to full feature set of Scheduler</span></span> |
| <span data-ttu-id="b6210-131">**P20 Premium**</span><span class="sxs-lookup"><span data-stu-id="b6210-131">**P20 Premium**</span></span> |<span data-ttu-id="b6210-132">每個作業集合 1000 個工作</span><span class="sxs-lookup"><span data-stu-id="b6210-132">1000 jobs per job collection</span></span> |<span data-ttu-id="b6210-133">每分鐘一次。</span><span class="sxs-lookup"><span data-stu-id="b6210-133">Once per minute.</span></span> <span data-ttu-id="b6210-134">執行工作不得超過一分鐘</span><span class="sxs-lookup"><span data-stu-id="b6210-134">Cannot execute jobs more often than once a minute</span></span> |<span data-ttu-id="b6210-135">一個訂用帳戶允許最多 10,000 個 P20 進階工作集合。</span><span class="sxs-lookup"><span data-stu-id="b6210-135">A subscription is allowed up to 10,000 P20 Premium job collections.</span></span> <span data-ttu-id="b6210-136">如需詳細資訊，請<a href="mailto:wapteams@microsoft.com">與我們連絡</a>。</span><span class="sxs-lookup"><span data-stu-id="b6210-136"><a href="mailto:wapteams@microsoft.com">Contact us</a> for more.</span></span> |<span data-ttu-id="b6210-137">存取排程器的完整功能集</span><span class="sxs-lookup"><span data-stu-id="b6210-137">Access to full feature set of Scheduler</span></span> |

## <a name="upgrades-and-downgrades-of-job-collection-plans"></a><span data-ttu-id="b6210-138">升級或降級工作集合計劃</span><span class="sxs-lookup"><span data-stu-id="b6210-138">Upgrades and Downgrades of Job Collection Plans</span></span>
<span data-ttu-id="b6210-139">您隨時可在免費、標準和高階計劃之間升級或降級工作集合計畫。</span><span class="sxs-lookup"><span data-stu-id="b6210-139">You may upgrade or downgrade a job collection plan anytime among the Free, Standard, and Premium plans.</span></span> <span data-ttu-id="b6210-140">不過，當降級至免費工作集合時，降級可能由於下列其中一個原因而失敗：</span><span class="sxs-lookup"><span data-stu-id="b6210-140">However, when downgrading to a free job collection, the downgrade may fail for one of the following reasons:</span></span>

* <span data-ttu-id="b6210-141">免費工作集合已存在於訂用帳戶中</span><span class="sxs-lookup"><span data-stu-id="b6210-141">A free job collection already exists in the subscription</span></span>
* <span data-ttu-id="b6210-142">工作集合中的工作有更高的週期，超過免費工作集合中工作允許的週期。</span><span class="sxs-lookup"><span data-stu-id="b6210-142">A job in the job collection has a higher recurrence than allowed for jobs in free job collections.</span></span> <span data-ttu-id="b6210-143">免費工作集合中允許的最大週期為每小時一次</span><span class="sxs-lookup"><span data-stu-id="b6210-143">The maximum recurrence allowed in a free job collection is once per hour</span></span>
* <span data-ttu-id="b6210-144">工作集合中有 5 個以上的工作</span><span class="sxs-lookup"><span data-stu-id="b6210-144">There are more than 5 jobs in the job collection</span></span>
* <span data-ttu-id="b6210-145">工作集合中的工作具有一個使用 [HTTP 輸出授權物件](scheduler-outbound-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b6210-145">A job in the job collection has an HTTP or HTTPS action that uses an [HTTP outbound authorization object](scheduler-outbound-authentication.md)</span></span>

## <a name="billing-and-azure-plans"></a><span data-ttu-id="b6210-146">計費與 Azure 計劃</span><span class="sxs-lookup"><span data-stu-id="b6210-146">Billing and Azure Plans</span></span>
<span data-ttu-id="b6210-147">不會對免費工作集合的訂用帳戶計費。</span><span class="sxs-lookup"><span data-stu-id="b6210-147">Subscriptions are not charged for free job collections.</span></span> <span data-ttu-id="b6210-148">如果您有 100 個以上的標準工作集合 (10 個標準計費單位)，則具有高階計劃中的所有工作集合，這是更好的方式。</span><span class="sxs-lookup"><span data-stu-id="b6210-148">If you have more than 100 standard job collections (10 standard billing units), then it's a better deal to have all job collections in the premium plan.</span></span>

<span data-ttu-id="b6210-149">如果有一個標準作業集合和一個高階作業集合，則您會支付一個標準計費單位「和」一個高階計費單位。</span><span class="sxs-lookup"><span data-stu-id="b6210-149">If you have one standard job collection and one premium job collection, you are billed one standard billing unit *and* one premium billing unit.</span></span> <span data-ttu-id="b6210-150">排程器服務會根據設定為標準或高階的作用中工作集合數目來計費；下兩節將有進一步的說明。</span><span class="sxs-lookup"><span data-stu-id="b6210-150">The Scheduler service bills based on the number of active job collections that are set to either standard or premium; this is explained further in the next two sections.</span></span>

## <a name="standard-billable-units"></a><span data-ttu-id="b6210-151">標準可計費單位</span><span class="sxs-lookup"><span data-stu-id="b6210-151">Standard Billable Units</span></span>
<span data-ttu-id="b6210-152">標準可計費單位可以包含最多 10 個標準工作集合。</span><span class="sxs-lookup"><span data-stu-id="b6210-152">A standard billable unit can include up to 10 standard job collections.</span></span> <span data-ttu-id="b6210-153">由於標準工作集合可以讓每個工作集合最多具有 50 個工作，因此一個標準計費單位可讓一個訂用帳戶最多具有 500 個工作 – 每個月幾乎高達 2 千 2 百萬個工作執行。</span><span class="sxs-lookup"><span data-stu-id="b6210-153">Since a standard job collection can have up to 50 jobs per job collection, one standard billing unit allows a subscription to have up to 500 jobs – up to almost 22 million job executions per month.</span></span>

<span data-ttu-id="b6210-154">如果有 1 到 10 個標準工作集合，則您將支付 1 個標準計費單位。</span><span class="sxs-lookup"><span data-stu-id="b6210-154">If you have between 1 and 10 standard job collections, you'll be billed for 1 standard billing unit.</span></span> <span data-ttu-id="b6210-155">如果有 11 到 20 個標準工作集合，則您將支付 2 個標準計費單位。</span><span class="sxs-lookup"><span data-stu-id="b6210-155">If you have between 11 and 20 standard job collections, you'll be billed for 2 standard billing units.</span></span> <span data-ttu-id="b6210-156">如果有 21 到 30 個標準工作集合，則您將支付 3 個標準計費單位。</span><span class="sxs-lookup"><span data-stu-id="b6210-156">If you have between 21 and 30 standard job collections, you'll be billed for 3 standard billing units, and so on.</span></span>

## <a name="p10-premium-billable-units"></a><span data-ttu-id="b6210-157">P10 進階可計費單位</span><span class="sxs-lookup"><span data-stu-id="b6210-157">P10 Premium Billable Units</span></span>
<span data-ttu-id="b6210-158">P10 進階可計費單位可以包含最多 10,000 個 P10 進階工作集合。</span><span class="sxs-lookup"><span data-stu-id="b6210-158">A P10 premium billable unit can include up to 10,000 P10 premium job collections.</span></span> <span data-ttu-id="b6210-159">由於 P10 進階工作集合可以讓每個工作集合最多具有 50 個工作，因此一個進階計費單位可讓一個訂用帳戶最多具有 500,000 個工作 – 每個月幾乎高達 220 億個工作執行。</span><span class="sxs-lookup"><span data-stu-id="b6210-159">Since a P10 premium job collection can have up to 50 jobs per job collection, one premium billing unit allows a subscription to have up to 500,000 jobs – up to almost 22 billion job executions per month.</span></span>

<span data-ttu-id="b6210-160">如果有 1 到 10,000 個進階工作集合，則您將支付 1 個 P10 進階計費單位。</span><span class="sxs-lookup"><span data-stu-id="b6210-160">If you have between 1 and 10,000 premium job collections, you'll be billed for 1 P10 premium billing unit.</span></span> <span data-ttu-id="b6210-161">如果有 10,001 到 20,000 個進階工作集合，則您將支付 2 個 P10 進階計費單位，依此類推。</span><span class="sxs-lookup"><span data-stu-id="b6210-161">If you have between 10,001 and 20,000 premium job collections, you'll be billed for 2 P10 premium billing units, and so on.</span></span>

<span data-ttu-id="b6210-162">因此，P10 進階工作集合具有與標準工作集合相同的功能，但萬一您的應用程式需要大量工作集合時提供折價。</span><span class="sxs-lookup"><span data-stu-id="b6210-162">Thus, P10 premium job collections have the same functionality as the standard job collections but provide a price break in case your application requires a lot of job collections.</span></span>

## <a name="p20-premium-billable-units"></a><span data-ttu-id="b6210-163">P20 進階可計費單位</span><span class="sxs-lookup"><span data-stu-id="b6210-163">P20 Premium Billable Units</span></span>
<span data-ttu-id="b6210-164">P20 進階可計費單位可以包含最多 5,000 個 P20 進階工作集合。</span><span class="sxs-lookup"><span data-stu-id="b6210-164">A P20 premium billable unit can include up to 5,000 P20 premium job collections.</span></span> <span data-ttu-id="b6210-165">由於 P20 進階工作集合可以讓每個工作集合最多具有 1,000 個工作，因此一個進階計費單位可讓一個訂用帳戶最多具有 5,000,000 個工作 – 每個月幾乎高達 2200 億個工作執行。</span><span class="sxs-lookup"><span data-stu-id="b6210-165">Since a P20 premium job collection can have up to 1,000 jobs per job collection, one premium billing unit allows a subscription to have up to 5,000,000 jobs – up to almost 220 billion job executions per month.</span></span>

<span data-ttu-id="b6210-166">P20 進階工作集合提供與 P10 進階工作集合相同的功能，但整體比起 P10 進階，每個工作集合支援更大量的工作數和更大量的工作總數，可讓您有更多的延展性。</span><span class="sxs-lookup"><span data-stu-id="b6210-166">P20 premium job collections provides the same capabilities as P10 premium job collections but also supports a greater number jobs per job collection and a greater total number of jobs overall than P10 premium allowing you to have more scalability.</span></span>

## <a name="billing-and-active-status"></a><span data-ttu-id="b6210-167">計費和作用中狀態</span><span class="sxs-lookup"><span data-stu-id="b6210-167">Billing and Active Status</span></span>
<span data-ttu-id="b6210-168">工作集合會永遠作用中，除非您整個訂用帳戶由於計費問題而進入部分暫時停用狀態。</span><span class="sxs-lookup"><span data-stu-id="b6210-168">Job collections are always active unless your entire subscription has gone into some temporary disabled state due to billing issues.</span></span> <span data-ttu-id="b6210-169">確保作業集合不計費的唯一方法，就是將它設定成「免費」計劃或刪除作業集合。</span><span class="sxs-lookup"><span data-stu-id="b6210-169">The only way to ensure that a job collection is not billed is to either set it to the *Free* plan or to delete the job collection.</span></span>

<span data-ttu-id="b6210-170">雖然您可能在單一作業中停用作業集合內的所有作業，但是它不會變更作業集合的計費狀態 – 作業集合「仍」會計費。</span><span class="sxs-lookup"><span data-stu-id="b6210-170">Although you may disable all jobs within a job collection in a single operation, it does not change the billing status of the job collection – the job collection will *still* be billed.</span></span> <span data-ttu-id="b6210-171">同樣地，空白的工作集合會被視為作用中，並將計費。</span><span class="sxs-lookup"><span data-stu-id="b6210-171">Similarly, empty job collections are considered active and will be billed.</span></span>

## <a name="pricing"></a><span data-ttu-id="b6210-172">價格</span><span class="sxs-lookup"><span data-stu-id="b6210-172">Pricing</span></span>
<span data-ttu-id="b6210-173">如需定價詳細資料，請參閱 [排程器定價](https://azure.microsoft.com/pricing/details/scheduler/)。</span><span class="sxs-lookup"><span data-stu-id="b6210-173">For pricing details, please see [Scheduler Pricing](https://azure.microsoft.com/pricing/details/scheduler/).</span></span>

## <a name="see-also"></a><span data-ttu-id="b6210-174">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b6210-174">See Also</span></span>
 [<span data-ttu-id="b6210-175">排程器是什麼？</span><span class="sxs-lookup"><span data-stu-id="b6210-175">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="b6210-176">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="b6210-176">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="b6210-177">在 Azure 入口網站中開始使用排程器</span><span class="sxs-lookup"><span data-stu-id="b6210-177">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="b6210-178">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="b6210-178">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="b6210-179">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="b6210-179">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="b6210-180">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="b6210-180">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="b6210-181">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="b6210-181">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="b6210-182">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="b6210-182">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

