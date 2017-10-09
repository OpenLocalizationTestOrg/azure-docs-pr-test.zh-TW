---
title: "服務網狀架構可靠狀態管理員和可靠的集合內部 aaaAzure |Microsoft 文件"
description: "深入了解 Reliable Collection 概念和 Azure Service Fabric 設計。"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: rajak
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: mcoskun
ms.openlocfilehash: 651bfb52785a2475e4840cd471e87220d1936391
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-reliable-state-manager-and-reliable-collection-internals"></a><span data-ttu-id="a87c4-103">Azure Service Fabric Reliable State Manager 與 Reliable Collection 內部</span><span class="sxs-lookup"><span data-stu-id="a87c4-103">Azure Service Fabric Reliable State Manager and Reliable Collection internals</span></span>
<span data-ttu-id="a87c4-104">這份文件是可靠的狀態管理員和可靠的集合 toosee 內探索核心元件 hello 幕後的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a87c4-104">This document delves inside Reliable State Manager and Reliable Collections toosee how core components work behind hello scenes.</span></span>

> [!NOTE]
> <span data-ttu-id="a87c4-105">這份文件仍在處理中。</span><span class="sxs-lookup"><span data-stu-id="a87c4-105">This document is work in-progress.</span></span> <span data-ttu-id="a87c4-106">加入註解 toothis 文章 tootell 我們主題，您想要深入了解 toolearn。</span><span class="sxs-lookup"><span data-stu-id="a87c4-106">Add comments toothis article tootell us what topic you would like toolearn more about.</span></span>
>

##  <a name="local-persistence-model-log-and-checkpoint"></a><span data-ttu-id="a87c4-107">本機持續性模型︰記錄和檢查點</span><span class="sxs-lookup"><span data-stu-id="a87c4-107">Local persistence model: log and checkpoint</span></span>
<span data-ttu-id="a87c4-108">hello 可靠狀態管理員和可靠的集合，請遵循稱為記錄檔和檢查點的持續性模型。</span><span class="sxs-lookup"><span data-stu-id="a87c4-108">hello Reliable State Manager and Reliable Collections follow a persistence model that is called Log and Checkpoint.</span></span>
<span data-ttu-id="a87c4-109">在此模型中，每個狀態變更會先記錄在磁碟上，然後套用在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="a87c4-109">In this model, each state change is logged on disk first and then applied in memory.</span></span>
<span data-ttu-id="a87c4-110">hello 完成本身被保存的狀態只是偶爾 （也稱為</span><span class="sxs-lookup"><span data-stu-id="a87c4-110">hello complete state itself is persisted only occasionally (a.k.a.</span></span> <span data-ttu-id="a87c4-111">檢查點)。</span><span class="sxs-lookup"><span data-stu-id="a87c4-111">Checkpoint).</span></span>
<span data-ttu-id="a87c4-112">hello 好處是差異會轉換成循序附加專用寫入磁碟上改善效能。</span><span class="sxs-lookup"><span data-stu-id="a87c4-112">hello benefit is that deltas are turned into sequential append-only writes on disk for improved performance.</span></span>

<span data-ttu-id="a87c4-113">toobetter 了解 hello 記錄和檢查點模型，讓我們先來看 hello 無限磁碟案例。</span><span class="sxs-lookup"><span data-stu-id="a87c4-113">toobetter understand hello Log and Checkpoint model, let’s first look at hello infinite disk scenario.</span></span>
<span data-ttu-id="a87c4-114">hello 可靠狀態管理員會記錄每項作業之前它會複寫。</span><span class="sxs-lookup"><span data-stu-id="a87c4-114">hello Reliable State Manager logs every operation before it is replicated.</span></span>
<span data-ttu-id="a87c4-115">記錄允許 hello 可靠集合 tooapply hello 作業只能在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="a87c4-115">Logging allows hello Reliable Collections tooapply hello operation only in memory.</span></span>
<span data-ttu-id="a87c4-116">因為記錄檔會保存，即使 hello 複本失敗且需要重新啟動，toobe hello 可靠狀態管理員有足夠的資訊在其記錄 tooreplay 所有 hello 作業 hello 複本都已遺失。</span><span class="sxs-lookup"><span data-stu-id="a87c4-116">Since logs are persisted, even when hello replica fails and needs toobe restarted, hello Reliable State Manager has enough information in its log tooreplay all hello operations hello replica has lost.</span></span>
<span data-ttu-id="a87c4-117">Hello 磁碟是無限的因為記錄檔記錄永遠不需要移除 toobe 且 hello 可靠集合必須 toomanage 唯一 hello 記憶體中狀態。</span><span class="sxs-lookup"><span data-stu-id="a87c4-117">As hello disk is infinite, log records never need toobe removed and hello Reliable Collection needs toomanage only hello in-memory state.</span></span>

<span data-ttu-id="a87c4-118">現在讓我們看看 hello 有限磁碟案例。</span><span class="sxs-lookup"><span data-stu-id="a87c4-118">Now let’s look at hello finite disk scenario.</span></span>
<span data-ttu-id="a87c4-119">因為記錄檔記錄會累積，hello 可靠狀態管理員將會用完磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="a87c4-119">As log records accumulate, hello Reliable State Manager will run out of disk space.</span></span>
<span data-ttu-id="a87c4-120">發生這種情況，hello 可靠狀態管理員必須 tootruncate 其記錄 toomake 出空間給 hello 較新記錄。</span><span class="sxs-lookup"><span data-stu-id="a87c4-120">Before that happens, hello Reliable State Manager needs tootruncate its log toomake room for hello newer records.</span></span>
<span data-ttu-id="a87c4-121">Reliable 狀態管理員要求在其記憶體中狀態 toodisk hello toocheckpoint 可靠的集合。</span><span class="sxs-lookup"><span data-stu-id="a87c4-121">Reliable State Manager requests hello Reliable Collections toocheckpoint their in-memory state toodisk.</span></span>
<span data-ttu-id="a87c4-122">此時，hello 可靠的集合' 會保存其記憶體中狀態。</span><span class="sxs-lookup"><span data-stu-id="a87c4-122">At this point, hello Reliable Collections' would persist its in-memory state.</span></span>
<span data-ttu-id="a87c4-123">Hello 可靠集合完成後的檢查點，hello 可靠狀態管理員可以截斷 hello 記錄 toofree 出磁碟空間。</span><span class="sxs-lookup"><span data-stu-id="a87c4-123">Once hello Reliable Collections complete their checkpoints, hello Reliable State Manager can truncate hello log toofree up disk space.</span></span>
<span data-ttu-id="a87c4-124">當 hello 複本需要重新啟動 toobe 時，可靠的集合會復原檢查點狀態，而且 hello 可靠狀態管理員復原播放 hello 最後一個檢查點之後發生的所有 hello 狀態變更。</span><span class="sxs-lookup"><span data-stu-id="a87c4-124">When hello replica needs toobe restarted, Reliable Collections recover their checkpointed state, and hello Reliable State Manager recovers and plays back all hello state changes that occurred since hello last checkpoint.</span></span>

<span data-ttu-id="a87c4-125">檢查點新增另一個值可改善一般情況下的復原時間。</span><span class="sxs-lookup"><span data-stu-id="a87c4-125">Another value add of checkpointing is that it improves recovery times in common scenarios.</span></span> <span data-ttu-id="a87c4-126">記錄檔包含 hello 最後一個檢查點之後發生的所有作業。</span><span class="sxs-lookup"><span data-stu-id="a87c4-126">Log contains all operations that have happened since hello last checkpoint.</span></span>
<span data-ttu-id="a87c4-127">因此它可能包含某個項目的多個版本，如 Reliable Dictionary 中特定資料列的多個值。</span><span class="sxs-lookup"><span data-stu-id="a87c4-127">So it may include multiple versions of an item like multiple values for a given row in Reliable Dictionary.</span></span>
<span data-ttu-id="a87c4-128">相反地，可靠的集合檢查點僅 hello 最新版本的每個索引鍵的值。</span><span class="sxs-lookup"><span data-stu-id="a87c4-128">In contrast, a Reliable Collection checkpoints only hello latest version of each value for a key.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a87c4-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a87c4-129">Next steps</span></span>
* [<span data-ttu-id="a87c4-130">交易和鎖定</span><span class="sxs-lookup"><span data-stu-id="a87c4-130">Transactions and Locks</span></span>](service-fabric-reliable-services-reliable-collections-transactions-locks.md)

