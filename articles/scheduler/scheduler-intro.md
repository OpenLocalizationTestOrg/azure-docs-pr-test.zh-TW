---
title: "何謂 Azure 排程器？ | Microsoft Docs"
description: "Azure 排程器可讓您以宣告方式描述在雲端中執行的動作。 然後它會排程這些動作並且自動執行。"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a3bf1aacd6978499d7ef77cbcb451a06b857ac38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="9c1b7-105">何謂 Azure 排程器？</span><span class="sxs-lookup"><span data-stu-id="9c1b7-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="9c1b7-106">Azure 排程器可讓您以宣告方式描述在雲端中執行的動作。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-106">Azure Scheduler allows you to declaratively describe actions to run in the cloud.</span></span> <span data-ttu-id="9c1b7-107">然後它會排程這些動作並且自動執行。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="9c1b7-108">排程器會使用 [Azure 入口網站](scheduler-get-started-portal.md)、程式碼、[REST API](https://msdn.microsoft.com/library/mt629143.aspx) 或 Azure PowerShell 來完成這個動作。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-108">Scheduler does this by using [the Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="9c1b7-109">排程器會建立、 維護和叫用已排程的工作。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="9c1b7-110">排程器不會裝載任何工作負載或執行任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="9c1b7-111">它只會叫用  其他位置裝載的程式碼：裝載於 Azure、內部部署或另一個提供者。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="9c1b7-112">它會透過 HTTP、HTTPS、儲存體佇列、服務匯流排佇列或服務匯流排主題叫用。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="9c1b7-113">排程器會排程 [工作](scheduler-concepts-terms.md)、保留使用者可以檢閱的工作執行結果歷程記錄，並且決定性地和可靠地排程要執行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads to be run.</span></span> <span data-ttu-id="9c1b7-114">Azure WebJobs (Azure App Service 之 Web Apps 功能的一部分) 和其他 Azure 排程功能會在背景使用排程器。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-114">Azure WebJobs (part of the Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in the background.</span></span> <span data-ttu-id="9c1b7-115">[排程器 REST API](https://msdn.microsoft.com/library/mt629143.aspx) 會協助管理這些動作的通訊。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-115">The [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage the communication for these actions.</span></span> <span data-ttu-id="9c1b7-116">因此，排程器可輕鬆地支援 [複雜的排程和進階週期](scheduler-advanced-complexity.md) 。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="9c1b7-117">需要使用排程器的案例有幾個。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-117">There are several scenarios that lend themselves to the usage of Scheduler.</span></span> <span data-ttu-id="9c1b7-118">例如：</span><span class="sxs-lookup"><span data-stu-id="9c1b7-118">For example:</span></span>

* <span data-ttu-id="9c1b7-119">週期性應用程式動作：定期將 Twitter 中的資料收集到摘要中。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="9c1b7-120">每日維護：每日剪除記錄、執行備份及其他維護工作。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="9c1b7-121">例如，系統管理員可以選擇早上 1:00 備份資料庫，</span><span class="sxs-lookup"><span data-stu-id="9c1b7-121">For example, an administrator may choose to back up the database at 1:00 A.M.</span></span> <span data-ttu-id="9c1b7-122">期間為接下來九個月的每天。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-122">every day for the next nine months.</span></span>

<span data-ttu-id="9c1b7-123">排程器可讓您使用指令碼，在入口網站中以程式設計方式建立、更新、刪除、檢視及管理工作和 [工作集合](scheduler-concepts-terms.md) 。</span><span class="sxs-lookup"><span data-stu-id="9c1b7-123">Scheduler allows you to create, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in the portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="9c1b7-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="9c1b7-124">See also</span></span>
 [<span data-ttu-id="9c1b7-125">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="9c1b7-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="9c1b7-126">在 Azure 入口網站中開始使用排程器</span><span class="sxs-lookup"><span data-stu-id="9c1b7-126">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="9c1b7-127">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="9c1b7-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="9c1b7-128">如何使用 Azure 排程器建立複雜的排程和進階週期</span><span class="sxs-lookup"><span data-stu-id="9c1b7-128">How to build complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="9c1b7-129">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="9c1b7-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="9c1b7-130">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="9c1b7-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="9c1b7-131">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="9c1b7-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="9c1b7-132">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="9c1b7-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="9c1b7-133">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="9c1b7-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

