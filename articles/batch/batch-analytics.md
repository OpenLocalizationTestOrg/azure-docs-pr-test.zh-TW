---
title: "aaaAzure 批次分析 |Microsoft 文件"
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
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a><span data-ttu-id="d8658-103">批次分析</span><span class="sxs-lookup"><span data-stu-id="d8658-103">Batch Analytics</span></span>
<span data-ttu-id="d8658-104">在批次分析中的 hello 主題包含 hello 事件和警示適用於批次服務資源的參考資訊。</span><span class="sxs-lookup"><span data-stu-id="d8658-104">hello topics in Batch Analytics contain reference information for hello events and alerts available for Batch service resources.</span></span>

<span data-ttu-id="d8658-105">請參閱[記錄事件以便對 Batch 解決方案進行診斷評估和監視](https://azure.microsoft.com/documentation/articles/batch-diagnostics/)，以取得啟用與取用批次診斷記錄檔的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d8658-105">See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="d8658-106">診斷記錄檔</span><span class="sxs-lookup"><span data-stu-id="d8658-106">Diagnostic logs</span></span>

<span data-ttu-id="d8658-107">hello Azure 批次服務會發出診斷記錄的事件遵循特定的資源，批次 hello 存留期間的 hello。</span><span class="sxs-lookup"><span data-stu-id="d8658-107">hello Azure Batch service emits hello following diagnostic log events during hello lifetime of certain Batch resources.</span></span>

<span data-ttu-id="d8658-108">**服務記錄檔事件**</span><span class="sxs-lookup"><span data-stu-id="d8658-108">**Service Log events**</span></span>
* [<span data-ttu-id="d8658-109">建立集區</span><span class="sxs-lookup"><span data-stu-id="d8658-109">Pool create</span></span>](batch-pool-create-event.md)
* [<span data-ttu-id="d8658-110">開始刪除集區</span><span class="sxs-lookup"><span data-stu-id="d8658-110">Pool delete start</span></span>](batch-pool-delete-start-event.md)
* [<span data-ttu-id="d8658-111">完成集區刪除</span><span class="sxs-lookup"><span data-stu-id="d8658-111">Pool delete complete</span></span>](batch-pool-delete-complete-event.md)
* [<span data-ttu-id="d8658-112">開始調整集區大小</span><span class="sxs-lookup"><span data-stu-id="d8658-112">Pool resize start</span></span>](batch-pool-resize-start-event.md)
* [<span data-ttu-id="d8658-113">完成集區大小調整</span><span class="sxs-lookup"><span data-stu-id="d8658-113">Pool resize complete</span></span>](batch-pool-resize-complete-event.md)
* [<span data-ttu-id="d8658-114">開始工作</span><span class="sxs-lookup"><span data-stu-id="d8658-114">Task start</span></span>](batch-task-start-event.md)
* [<span data-ttu-id="d8658-115">完成工作</span><span class="sxs-lookup"><span data-stu-id="d8658-115">Task complete</span></span>](batch-task-complete-event.md)
* [<span data-ttu-id="d8658-116">工作失敗</span><span class="sxs-lookup"><span data-stu-id="d8658-116">Task fail</span></span>](batch-task-fail-event.md)