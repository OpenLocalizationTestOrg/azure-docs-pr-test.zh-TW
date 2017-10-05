---
title: "Azure Batch 集區刪除完成事件 | Microsoft Docs"
description: "Batch 集區刪除完成事件的參考。"
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
ms.openlocfilehash: 890f2ba7fda37060c56177868d6214d517d91831
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="275ee-103">集區刪除完成事件</span><span class="sxs-lookup"><span data-stu-id="275ee-103">Pool delete complete event</span></span>

 <span data-ttu-id="275ee-104">集區刪除作業完成時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="275ee-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="275ee-105">下列事件顯示集區刪除完成事件內文。</span><span class="sxs-lookup"><span data-stu-id="275ee-105">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="275ee-106">元素</span><span class="sxs-lookup"><span data-stu-id="275ee-106">Element</span></span>|<span data-ttu-id="275ee-107">類型</span><span class="sxs-lookup"><span data-stu-id="275ee-107">Type</span></span>|<span data-ttu-id="275ee-108">注意事項</span><span class="sxs-lookup"><span data-stu-id="275ee-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="275ee-109">id</span><span class="sxs-lookup"><span data-stu-id="275ee-109">id</span></span>|<span data-ttu-id="275ee-110">String</span><span class="sxs-lookup"><span data-stu-id="275ee-110">String</span></span>|<span data-ttu-id="275ee-111">集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="275ee-111">The id of the pool.</span></span>|
|<span data-ttu-id="275ee-112">startTime</span><span class="sxs-lookup"><span data-stu-id="275ee-112">startTime</span></span>|<span data-ttu-id="275ee-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="275ee-113">DateTime</span></span>|<span data-ttu-id="275ee-114">集區刪除開始時間。</span><span class="sxs-lookup"><span data-stu-id="275ee-114">The time the pool delete started.</span></span>|
|<span data-ttu-id="275ee-115">EndTime</span><span class="sxs-lookup"><span data-stu-id="275ee-115">endTime</span></span>|<span data-ttu-id="275ee-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="275ee-116">DateTime</span></span>|<span data-ttu-id="275ee-117">集區刪除完成時間。</span><span class="sxs-lookup"><span data-stu-id="275ee-117">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="275ee-118">備註</span><span class="sxs-lookup"><span data-stu-id="275ee-118">Remarks</span></span>
<span data-ttu-id="275ee-119">如需集區調整大小作業狀態與錯誤碼的詳細資訊，請參閱[將集區自帳戶中刪除](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account) (英文)</span><span class="sxs-lookup"><span data-stu-id="275ee-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>