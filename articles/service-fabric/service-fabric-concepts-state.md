---
title: "定義及管理 Azure 微服務中的狀態 |Microsoft Docs"
description: "如何定義和管理 Service Fabric 中的服務狀態"
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
ms.openlocfilehash: 2f7835fab175bdb7ef7ce3894cab9e09a39457f3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="service-state"></a><span data-ttu-id="4bd1e-103">服務狀態</span><span class="sxs-lookup"><span data-stu-id="4bd1e-103">Service state</span></span>
<span data-ttu-id="4bd1e-104">「服務狀態」係指服務正常運作所需的記憶體或磁碟資料。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-104">**Service state** refers to the in-memory or on disk data that a service requires to function.</span></span> <span data-ttu-id="4bd1e-105">例如，其包括可以讓服務讀取及寫入，以執行工作的資料結構及成員變數。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-105">It includes, for example, the data structures and member variables that the service reads and writes to do work.</span></span> <span data-ttu-id="4bd1e-106">根據服務的架構方式而定，它可能還包括儲存在磁碟上的檔案或其他資源。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-106">Depending on how the service is architected, it could also include files or other resources that are stored on disk.</span></span> <span data-ttu-id="4bd1e-107">例如，資料庫要用於儲存資料和交易記錄的檔案。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-107">For example, the files a database would use to store data and transaction logs.</span></span>

<span data-ttu-id="4bd1e-108">作為範例服務，讓我們考慮計算機。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-108">As an example service, let's consider a calculator.</span></span> <span data-ttu-id="4bd1e-109">基本計算機服務會採用兩個數字並傳回其總和。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-109">A basic calculator service takes two numbers and returns their sum.</span></span> <span data-ttu-id="4bd1e-110">執行這項計算不會牽涉任何成員變數或其他資訊。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-110">Performing this calculation involves no member variables or other information.</span></span>

<span data-ttu-id="4bd1e-111">現在，假設相同的計算機，但包含其他方法可以儲存並傳回上一個計算總和。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-111">Now consider the same calculator, but with an additional method for storing and returning the last sum it has computed.</span></span> <span data-ttu-id="4bd1e-112">此服務現在為具狀態。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-112">This service is now stateful.</span></span> <span data-ttu-id="4bd1e-113">具狀態表示其中包含當其計算新的總和時，某些要寫入的狀態，和當您要求其傳回最後一個已計算總和時，要讀取的狀態。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-113">Stateful means it contains some state that it writes to when it computes a new sum and reads from when you ask it to return the last computed sum.</span></span>

<span data-ttu-id="4bd1e-114">在 Azure Service Fabric 中，第一個服務稱為無狀態服務。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-114">In Azure Service Fabric, the first service is called a stateless service.</span></span> <span data-ttu-id="4bd1e-115">第二個服務稱為可設定狀態的服務。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-115">The second service is called a stateful service.</span></span>

## <a name="storing-service-state"></a><span data-ttu-id="4bd1e-116">儲存服務狀態</span><span class="sxs-lookup"><span data-stu-id="4bd1e-116">Storing service state</span></span>
<span data-ttu-id="4bd1e-117">狀態可進行外部化，也可並存在運作該狀態的程式碼中。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-117">State can be either externalized or co-located with the code that is manipulating the state.</span></span> <span data-ttu-id="4bd1e-118">狀態外部化的做法通常是使用外部資料庫，或是透過網路在不同電腦上或在相同電腦上的流程以外執行的其他資料存放區。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-118">Externalization of state is typically done by using an external database or other data store that runs on different machines over the network or out of process on the same machine.</span></span> <span data-ttu-id="4bd1e-119">在計算機範例中，資料存放區可能是 SQL Database 或 Azure 資料表存放區的執行個體。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-119">In our calculator example, the data store could be a SQL database or instance of Azure Table Store.</span></span> <span data-ttu-id="4bd1e-120">計算總和的每個要求都會執行此資料的更新，且要求服務傳回值會造成從存放區擷取目前的值。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-120">Every request to compute the sum performs an update on this data, and requests to the service to return the value result in the current value being fetched from the store.</span></span> 

<span data-ttu-id="4bd1e-121">狀態也可以使用操作狀態的程式碼進行共置。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-121">State can also be co-located with the code that manipulates the state.</span></span> <span data-ttu-id="4bd1e-122">Service Fabric 中的具狀態服務通常是使用此模型來建置。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-122">Stateful services in Service Fabric are typically built using this model.</span></span> <span data-ttu-id="4bd1e-123">Service Fabric 提供的基礎結構可確保此狀態是高度可用、一致且持久，且使用這種方式建置的服務可以輕鬆地加以縮放。</span><span class="sxs-lookup"><span data-stu-id="4bd1e-123">Service Fabric provides the infrastructure to ensure that this state is highly available, consistent, and durable, and that the services built this way can easily scale.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bd1e-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bd1e-124">Next steps</span></span>
<span data-ttu-id="4bd1e-125">如需有關 Service Fabric 概念的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="4bd1e-125">For more information on Service Fabric concepts, see the following articles:</span></span>

* [<span data-ttu-id="4bd1e-126">Service Fabric 服務的可用性</span><span class="sxs-lookup"><span data-stu-id="4bd1e-126">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="4bd1e-127">Service Fabric 服務的延展性</span><span class="sxs-lookup"><span data-stu-id="4bd1e-127">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="4bd1e-128">分割 Service Fabric 服務</span><span class="sxs-lookup"><span data-stu-id="4bd1e-128">Partitioning Service Fabric services</span></span>](service-fabric-concepts-partitioning.md)
* [<span data-ttu-id="4bd1e-129">Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="4bd1e-129">Service Fabric Reliable Services</span></span>](service-fabric-reliable-services-introduction.md)
