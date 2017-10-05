---
title: "Azure Batch 集區刪除開始事件 | Microsoft Docs"
description: "Batch 集區刪除開始事件的參考。"
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
ms.openlocfilehash: f8a5241dce422e5c826ab428da6d7bc93284a1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="2702a-103">集區刪除開始事件</span><span class="sxs-lookup"><span data-stu-id="2702a-103">Pool delete start event</span></span>

 <span data-ttu-id="2702a-104">集區刪除作業開始時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="2702a-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="2702a-105">由於集區刪除為非同步事件，因此您可以預期當刪除作業完成時，就會發出集區刪除完成事件。</span><span class="sxs-lookup"><span data-stu-id="2702a-105">Since the pool delete is an asynchronous event, you can expect a pool delete complete event to be emitted once the delete operation completes.</span></span>

 <span data-ttu-id="2702a-106">下列範例顯示集區刪除開始事件內文。</span><span class="sxs-lookup"><span data-stu-id="2702a-106">The following example shows the body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="2702a-107">元素</span><span class="sxs-lookup"><span data-stu-id="2702a-107">Element</span></span>|<span data-ttu-id="2702a-108">類型</span><span class="sxs-lookup"><span data-stu-id="2702a-108">Type</span></span>|<span data-ttu-id="2702a-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="2702a-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="2702a-110">id</span><span class="sxs-lookup"><span data-stu-id="2702a-110">id</span></span>|<span data-ttu-id="2702a-111">String</span><span class="sxs-lookup"><span data-stu-id="2702a-111">String</span></span>|<span data-ttu-id="2702a-112">集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="2702a-112">The id of the pool.</span></span>|