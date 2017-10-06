---
title: "aaa\"Azure Batch 集區刪除完成事件 |Microsoft 文件 」"
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
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="11109-103">集區刪除完成事件</span><span class="sxs-lookup"><span data-stu-id="11109-103">Pool delete complete event</span></span>

 <span data-ttu-id="11109-104">集區刪除作業完成時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="11109-104">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="11109-105">hello 下列範例顯示 hello 主體的集區刪除完成事件。</span><span class="sxs-lookup"><span data-stu-id="11109-105">hello following example shows hello body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="11109-106">元素</span><span class="sxs-lookup"><span data-stu-id="11109-106">Element</span></span>|<span data-ttu-id="11109-107">類型</span><span class="sxs-lookup"><span data-stu-id="11109-107">Type</span></span>|<span data-ttu-id="11109-108">注意事項</span><span class="sxs-lookup"><span data-stu-id="11109-108">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="11109-109">id</span><span class="sxs-lookup"><span data-stu-id="11109-109">id</span></span>|<span data-ttu-id="11109-110">String</span><span class="sxs-lookup"><span data-stu-id="11109-110">String</span></span>|<span data-ttu-id="11109-111">hello hello 集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="11109-111">hello id of hello pool.</span></span>|
|<span data-ttu-id="11109-112">startTime</span><span class="sxs-lookup"><span data-stu-id="11109-112">startTime</span></span>|<span data-ttu-id="11109-113">DateTime</span><span class="sxs-lookup"><span data-stu-id="11109-113">DateTime</span></span>|<span data-ttu-id="11109-114">hello 集區刪除的 hello 時間啟動。</span><span class="sxs-lookup"><span data-stu-id="11109-114">hello time hello pool delete started.</span></span>|
|<span data-ttu-id="11109-115">EndTime</span><span class="sxs-lookup"><span data-stu-id="11109-115">endTime</span></span>|<span data-ttu-id="11109-116">DateTime</span><span class="sxs-lookup"><span data-stu-id="11109-116">DateTime</span></span>|<span data-ttu-id="11109-117">hello hello 集區刪除完成的時間。</span><span class="sxs-lookup"><span data-stu-id="11109-117">hello time hello pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="11109-118">備註</span><span class="sxs-lookup"><span data-stu-id="11109-118">Remarks</span></span>
<span data-ttu-id="11109-119">如需集區調整大小作業狀態與錯誤碼的詳細資訊，請參閱[將集區自帳戶中刪除](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account) (英文)</span><span class="sxs-lookup"><span data-stu-id="11109-119">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>