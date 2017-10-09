---
title: "aaaDefinine 和管理 Azure microservices 狀態 |Microsoft 文件"
description: "如何 toodefine 和管理服務的網狀架構中的服務狀態"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a><span data-ttu-id="2f35c-103">服務狀態</span><span class="sxs-lookup"><span data-stu-id="2f35c-103">Service state</span></span>
<span data-ttu-id="2f35c-104">**服務狀態**參考 toohello 記憶體或磁碟資料服務需要 toofunction。</span><span class="sxs-lookup"><span data-stu-id="2f35c-104">**Service state** refers toohello in-memory or on disk data that a service requires toofunction.</span></span> <span data-ttu-id="2f35c-105">它包含，例如 hello 資料結構和成員變數 hello 服務讀取和寫入 toodo 工作。</span><span class="sxs-lookup"><span data-stu-id="2f35c-105">It includes, for example, hello data structures and member variables that hello service reads and writes toodo work.</span></span> <span data-ttu-id="2f35c-106">根據如何 hello 服務的架構，它也可能包括檔案或儲存在磁碟的其他資源。</span><span class="sxs-lookup"><span data-stu-id="2f35c-106">Depending on how hello service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="2f35c-107">Hello，例如檔案的資料庫會使用 toostore 資料和交易記錄。</span><span class="sxs-lookup"><span data-stu-id="2f35c-107">For example, hello files a database would use toostore data and transaction logs.</span></span>

<span data-ttu-id="2f35c-108">作為範例服務，讓我們考慮計算機。</span><span class="sxs-lookup"><span data-stu-id="2f35c-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="2f35c-109">基本計算機服務會採用兩個數字並傳回其總和。</span><span class="sxs-lookup"><span data-stu-id="2f35c-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="2f35c-110">執行這項計算不會牽涉任何成員變數或其他資訊。</span><span class="sxs-lookup"><span data-stu-id="2f35c-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="2f35c-111">現在請思考一下 hello 相同的計算機，但已經使用其他方法來儲存及傳回 hello 最後一個加總計算。</span><span class="sxs-lookup"><span data-stu-id="2f35c-111">Now consider hello same calculator, but with an additional method for storing and returning hello last sum it has computed.</span></span> <span data-ttu-id="2f35c-112">此服務現在為具狀態。</span><span class="sxs-lookup"><span data-stu-id="2f35c-112">This service is now stateful.</span></span> <span data-ttu-id="2f35c-113">可設定狀態，表示它包含寫入的 toowhen，它會計算新的總和，並讀取時詢問 tooreturn hello 的最後一個計算的總和的某種狀態。</span><span class="sxs-lookup"><span data-stu-id="2f35c-113">Stateful means it contains some state that it writes toowhen it computes a new sum and reads from when you ask it tooreturn hello last computed sum.</span></span>

<span data-ttu-id="2f35c-114">在 Azure Service Fabric，hello 第一個服務稱為無狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="2f35c-114">In Azure Service Fabric, hello first service is called a stateless service.</span></span> <span data-ttu-id="2f35c-115">hello 第二個服務會呼叫可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="2f35c-115">hello second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="2f35c-116">儲存服務狀態</span><span class="sxs-lookup"><span data-stu-id="2f35c-116">Storing service state</span></span>
<span data-ttu-id="2f35c-117">狀態可以外部化或共置 hello 程式碼，它會處理 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="2f35c-117">State can be either externalized or co-located with hello code that is manipulating hello state.</span></span> <span data-ttu-id="2f35c-118">外部化的狀態通常是使用外部資料庫或其他資料存放區 hello 網路上或跨處理序上的不同電腦上執行 hello 同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="2f35c-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over hello network or out of process on hello same machine.</span></span> <span data-ttu-id="2f35c-119">在計算機範例中，SQL database 或 Azure 資料表存放區執行個體，可能是 hello 資料存放區。</span><span class="sxs-lookup"><span data-stu-id="2f35c-119">In our calculator example, hello data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="2f35c-120">每個要求 toocompute hello 加總這個資料中，執行更新，並要求 toohello 服務 tooreturn hello 值導致 hello 提取從 hello 存放區的目前值。</span><span class="sxs-lookup"><span data-stu-id="2f35c-120">Every request toocompute hello sum performs an update on this data, and requests toohello service tooreturn hello value result in hello current value being fetched from hello store.</span></span> 

<span data-ttu-id="2f35c-121">狀態也可以共置於 hello 操作 hello 狀態的程式碼。</span><span class="sxs-lookup"><span data-stu-id="2f35c-121">State can also be co-located with hello code that manipulates hello state.</span></span> <span data-ttu-id="2f35c-122">Service Fabric 中的具狀態服務通常是使用此模型來建置。</span><span class="sxs-lookup"><span data-stu-id="2f35c-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="2f35c-123">Service Fabric 提供 hello 基礎結構 tooensure 此狀態是高度可用、 一致且持久，，和 hello services 內建這種方式可以輕鬆地調整。</span><span class="sxs-lookup"><span data-stu-id="2f35c-123">Service Fabric provides hello infrastructure tooensure that this state is highly available, consistent, and durable, and that hello services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f35c-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f35c-124">Next steps</span></span>
<span data-ttu-id="2f35c-125">如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="2f35c-125">For more information on Service Fabric concepts, see hello following articles:</span></span>

* [<span data-ttu-id="2f35c-126">Service Fabric 服務的可用性</span><span class="sxs-lookup"><span data-stu-id="2f35c-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="2f35c-127">Service Fabric 服務的延展性</span><span class="sxs-lookup"><span data-stu-id="2f35c-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="2f35c-128">分割 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="2f35c-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="2f35c-129">Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="2f35c-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
