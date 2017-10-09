---
title: "aaaWhat 是 Azure 排程器？ | Microsoft Docs"
description: "Azure 排程器可讓您 toodeclaratively 描述動作 toorun hello 雲端中的。 然後它會排程這些動作並且自動執行。"
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
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="12a3a-105">何謂 Azure 排程器？</span><span class="sxs-lookup"><span data-stu-id="12a3a-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="12a3a-106">Azure 排程器可讓您 toodeclaratively 描述動作 toorun hello 雲端中的。</span><span class="sxs-lookup"><span data-stu-id="12a3a-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="12a3a-107">然後它會排程這些動作並且自動執行。</span><span class="sxs-lookup"><span data-stu-id="12a3a-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="12a3a-108">排程器的做法是使用[hello Azure 入口網站](scheduler-get-started-portal.md)，程式碼中， [REST API](https://msdn.microsoft.com/library/mt629143.aspx)，或 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="12a3a-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="12a3a-109">排程器會建立、 維護和叫用已排程的工作。</span><span class="sxs-lookup"><span data-stu-id="12a3a-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="12a3a-110">排程器不會裝載任何工作負載或執行任何程式碼。</span><span class="sxs-lookup"><span data-stu-id="12a3a-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="12a3a-111">它只會叫用  其他位置裝載的程式碼：裝載於 Azure、內部部署或另一個提供者。</span><span class="sxs-lookup"><span data-stu-id="12a3a-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="12a3a-112">它會透過 HTTP、HTTPS、儲存體佇列、服務匯流排佇列或服務匯流排主題叫用。</span><span class="sxs-lookup"><span data-stu-id="12a3a-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="12a3a-113">排程器排程[作業](scheduler-concepts-terms.md)，會保留工作執行結果的其中一個可以檢閱，並排程工作負載 toobe 決定性且可靠地執行。</span><span class="sxs-lookup"><span data-stu-id="12a3a-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="12a3a-114">Azure WebJobs （hello Azure App Service 中的 Web 應用程式功能的一部分） 和其他 Azure 排程功能使用排程器在 hello 背景。</span><span class="sxs-lookup"><span data-stu-id="12a3a-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="12a3a-115">hello[排程器 REST API](https://msdn.microsoft.com/library/mt629143.aspx)可協助管理這些動作的 hello 通訊。</span><span class="sxs-lookup"><span data-stu-id="12a3a-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="12a3a-116">因此，排程器可輕鬆地支援 [複雜的排程和進階週期](scheduler-advanced-complexity.md) 。</span><span class="sxs-lookup"><span data-stu-id="12a3a-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="12a3a-117">有數個應用程式為自己的排程器的 toohello 用法的案例。</span><span class="sxs-lookup"><span data-stu-id="12a3a-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="12a3a-118">例如：</span><span class="sxs-lookup"><span data-stu-id="12a3a-118">For example:</span></span>

* <span data-ttu-id="12a3a-119">週期性應用程式動作：定期將 Twitter 中的資料收集到摘要中。</span><span class="sxs-lookup"><span data-stu-id="12a3a-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="12a3a-120">每日維護：每日剪除記錄、執行備份及其他維護工作。</span><span class="sxs-lookup"><span data-stu-id="12a3a-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="12a3a-121">例如，系統管理員可以選擇 tooback hello 資料庫上午 1:00</span><span class="sxs-lookup"><span data-stu-id="12a3a-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="12a3a-122">每日 hello 未來 9 個月。</span><span class="sxs-lookup"><span data-stu-id="12a3a-122">every day for hello next nine months.</span></span>

<span data-ttu-id="12a3a-123">排程器可讓您 toocreate、 更新、 刪除、 檢視和管理工作和[工作集合](scheduler-concepts-terms.md)以程式設計的方式，利用指令碼，並在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="12a3a-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="12a3a-124">另請參閱</span><span class="sxs-lookup"><span data-stu-id="12a3a-124">See also</span></span>
 [<span data-ttu-id="12a3a-125">Azure 排程器概念、術語及實體階層</span><span class="sxs-lookup"><span data-stu-id="12a3a-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="12a3a-126">開始在 hello Azure 入口網站中使用排程器</span><span class="sxs-lookup"><span data-stu-id="12a3a-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="12a3a-127">Azure 排程器的計劃和計費</span><span class="sxs-lookup"><span data-stu-id="12a3a-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="12a3a-128">排程 toobuild 複雜的方式與進階循環使用 Azure 排程器</span><span class="sxs-lookup"><span data-stu-id="12a3a-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="12a3a-129">Azure 排程器 REST API 參考</span><span class="sxs-lookup"><span data-stu-id="12a3a-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="12a3a-130">Azure 排程器 PowerShell Cmdlet 參考</span><span class="sxs-lookup"><span data-stu-id="12a3a-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="12a3a-131">Azure 排程器高可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="12a3a-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="12a3a-132">Azure 排程器限制、預設值和錯誤碼</span><span class="sxs-lookup"><span data-stu-id="12a3a-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="12a3a-133">Azure 排程器輸出驗證</span><span class="sxs-lookup"><span data-stu-id="12a3a-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

