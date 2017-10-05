---
title: "Azure Batch 分析 | Microsoft Docs"
description: "Azure Batch 分析的參考。"
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 7d634e1bb595a84b8af339e5bc5a483a7849e7f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="7ccae-103">批次分析</span><span class="sxs-lookup"><span data-stu-id="7ccae-103">Batch Analytics</span></span>
<span data-ttu-id="7ccae-104">批次分析中的主題包含批次服務資源所適用事件和警示的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="7ccae-104">The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="7ccae-105">請參閱[記錄事件以便對 Batch 解決方案進行診斷評估和監視](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)，以取得啟用與取用批次診斷記錄檔的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7ccae-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="7ccae-106">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="7ccae-106">Diagnostic logs</span></span>

<span data-ttu-id="7ccae-107">Azure 批次服務會在某些批次資源的存留期間發出下列診斷記錄事件。</span><span class="sxs-lookup"><span data-stu-id="7ccae-107">The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.</span></span>

<span data-ttu-id="7ccae-108">**服務記錄檔事件**</span><span class="sxs-lookup"><span data-stu-id="7ccae-108">**Service Log events**</span></span>
* [<span data-ttu-id="7ccae-109">建立集區</span><span class="sxs-lookup"><span data-stu-id="7ccae-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="7ccae-110">開始刪除集區</span><span class="sxs-lookup"><span data-stu-id="7ccae-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="7ccae-111">完成集區刪除</span><span class="sxs-lookup"><span data-stu-id="7ccae-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="7ccae-112">開始調整集區大小</span><span class="sxs-lookup"><span data-stu-id="7ccae-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="7ccae-113">完成集區大小調整</span><span class="sxs-lookup"><span data-stu-id="7ccae-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="7ccae-114">開始工作</span><span class="sxs-lookup"><span data-stu-id="7ccae-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="7ccae-115">完成工作</span><span class="sxs-lookup"><span data-stu-id="7ccae-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="7ccae-116">工作失敗</span><span class="sxs-lookup"><span data-stu-id="7ccae-116">Task fail</span></span>](batch-task-fail-event.md)