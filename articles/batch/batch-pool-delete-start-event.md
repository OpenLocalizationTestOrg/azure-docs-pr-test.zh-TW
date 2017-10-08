---
title: "aaa\"Azure Batch 集區刪除開始事件 |Microsoft 文件 」"
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a><span data-ttu-id="b2fbb-103">集區刪除開始事件</span><span class="sxs-lookup"><span data-stu-id="b2fbb-103">Pool delete start event</span></span>

 <span data-ttu-id="b2fbb-104">集區刪除作業開始時，就會發出此事件。</span><span class="sxs-lookup"><span data-stu-id="b2fbb-104">This event is emitted when a pool delete operation has started.</span></span> <span data-ttu-id="b2fbb-105">由於 hello 集區刪除非同步事件，您可以預期發出一次 hello 刪除作業的集區刪除完成事件 toobe 完成。</span><span class="sxs-lookup"><span data-stu-id="b2fbb-105">Since hello pool delete is an asynchronous event, you can expect a pool delete complete event toobe emitted once hello delete operation completes.</span></span>

 <span data-ttu-id="b2fbb-106">hello 下列範例顯示 hello 主體的集區刪除開始事件。</span><span class="sxs-lookup"><span data-stu-id="b2fbb-106">hello following example shows hello body of a pool delete start event.</span></span>

```
{
    "id": "myPool1"
}
```

|<span data-ttu-id="b2fbb-107">元素</span><span class="sxs-lookup"><span data-stu-id="b2fbb-107">Element</span></span>|<span data-ttu-id="b2fbb-108">類型</span><span class="sxs-lookup"><span data-stu-id="b2fbb-108">Type</span></span>|<span data-ttu-id="b2fbb-109">注意事項</span><span class="sxs-lookup"><span data-stu-id="b2fbb-109">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="b2fbb-110">id</span><span class="sxs-lookup"><span data-stu-id="b2fbb-110">id</span></span>|<span data-ttu-id="b2fbb-111">String</span><span class="sxs-lookup"><span data-stu-id="b2fbb-111">String</span></span>|<span data-ttu-id="b2fbb-112">hello hello 集區識別碼。</span><span class="sxs-lookup"><span data-stu-id="b2fbb-112">hello id of hello pool.</span></span>|
