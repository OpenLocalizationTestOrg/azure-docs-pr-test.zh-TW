---
title: "Service Fabric 程式撰寫模型概觀 | Microsoft Docs"
description: "Service Fabric 提供兩種架構來建置服務：動作項目架構和服務架構。 它們在簡化與控制中提供不同的取捨。"
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: vturecek
ms.assetid: 974b2614-014e-4587-a947-28fcef28b382
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: vturecek
ms.openlocfilehash: ca36f42897cd44d6da1a3cb6db53f656cf6256ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-programming-model-overview"></a><span data-ttu-id="406ad-104">Service Fabric 程式設計模型概觀</span><span class="sxs-lookup"><span data-stu-id="406ad-104">Service Fabric programming model overview</span></span>
<span data-ttu-id="406ad-105">Service Fabric 提供多種撰寫和管理服務的方式。</span><span class="sxs-lookup"><span data-stu-id="406ad-105">Service Fabric offers multiple ways to write and manage your services.</span></span> <span data-ttu-id="406ad-106">服務可選擇使用 Service Fabric API 以善加運用平台的功能和應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="406ad-106">Services can choose to use the Service Fabric APIs to take full advantage of the platform's features and application frameworks.</span></span> <span data-ttu-id="406ad-107">服務也可以是以任何語言撰寫的任何已編譯可執行程式，或是在 Service Fabric 叢集所裝載之容器中執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="406ad-107">Services can also be any compiled executable program written in any language or code running in a container simply hosted on a Service Fabric cluster.</span></span>

## <a name="guest-executables"></a><span data-ttu-id="406ad-108">客體可執行檔</span><span class="sxs-lookup"><span data-stu-id="406ad-108">Guest executables</span></span>
<span data-ttu-id="406ad-109">[客體可執行檔](service-fabric-deploy-existing-app.md)是可在應用程式中作為服務執行的現有任意可執行檔 (以任何語言撰寫)。</span><span class="sxs-lookup"><span data-stu-id="406ad-109">A [guest executable](service-fabric-deploy-existing-app.md) is an existing, arbitrary executable (written in any language) that can be run as a service in your application.</span></span> <span data-ttu-id="406ad-110">客體可執行檔不直接呼叫 Service Fabric SDK API。</span><span class="sxs-lookup"><span data-stu-id="406ad-110">Guest executables do not call the Service Fabric SDK APIs directly.</span></span> <span data-ttu-id="406ad-111">不過，它們仍然受惠於功能和平台提供項目，例如透過呼叫 Service Fabric 公開的 REST API 使用探索服務、自訂健康情況和負載報告。</span><span class="sxs-lookup"><span data-stu-id="406ad-111">However they still benefit from features the platform offers, such as service discoverability, custom health and load reporting by calling REST APIs exposed by Service Fabric.</span></span> <span data-ttu-id="406ad-112">它們也具備完整的應用程式生命週期支援。</span><span class="sxs-lookup"><span data-stu-id="406ad-112">They also have full application lifecycle support.</span></span>

<span data-ttu-id="406ad-113">部署您的第一個 [來賓可執行的應用程式](service-fabric-deploy-existing-app.md)，開始使用來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="406ad-113">Get started with guest executables by deploying your first [guest executable application](service-fabric-deploy-existing-app.md).</span></span>

## <a name="containers"></a><span data-ttu-id="406ad-114">容器</span><span class="sxs-lookup"><span data-stu-id="406ad-114">Containers</span></span>
<span data-ttu-id="406ad-115">根據預設，Service Fabric 會以處理程序形式部署和啟用這些服務。</span><span class="sxs-lookup"><span data-stu-id="406ad-115">By default, Service Fabric deploys and activates services as processes.</span></span> <span data-ttu-id="406ad-116">Service Fabric 也可以在[容器](service-fabric-containers-overview.md)中部署服務。</span><span class="sxs-lookup"><span data-stu-id="406ad-116">Service Fabric can also deploy services in [containers](service-fabric-containers-overview.md).</span></span> <span data-ttu-id="406ad-117">Service Fabric 支援在 Windows Server 2016 上部署 Linux 容器和 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="406ad-117">Service Fabric supports deployment of Linux containers and Windows containers on Windows Server 2016.</span></span> <span data-ttu-id="406ad-118">可以從任何容器存放庫提取容器映像，並部署至機器。</span><span class="sxs-lookup"><span data-stu-id="406ad-118">Container images can be pulled from any container repository and deployed to the machine.</span></span> <span data-ttu-id="406ad-119">您可以在容器中部署現有的應用程式成為客體可執行檔、Service Fabric 無狀態或具狀態 Reliable Services，或 Reliable Actors，並且可以在同一個應用程式中混合使用處理序中的服務和容器中的服務。</span><span class="sxs-lookup"><span data-stu-id="406ad-119">You can deploy existing applications as guest exectuables, Service Fabric stateless or stateful Reliable services or Reliable Actors in containers, and you can mix services in processes and services in containers in the same application.</span></span>

[<span data-ttu-id="406ad-120">深入了解如何在 Windows 或 Linux 中將服務容器化</span><span class="sxs-lookup"><span data-stu-id="406ad-120">Learn more about containerizing your services in Windows or Linux</span></span>](service-fabric-deploy-container.md)

## <a name="reliable-services"></a><span data-ttu-id="406ad-121">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="406ad-121">Reliable Services</span></span>
<span data-ttu-id="406ad-122">Reliable Services 是輕量級的服務撰寫架構，這些服務與 Service Fabric 平台整合，並得益於完整的平台功能。</span><span class="sxs-lookup"><span data-stu-id="406ad-122">Reliable Services is a light-weight framework for writing services that integrate with the Service Fabric platform and benefit from the full set of platform features.</span></span> <span data-ttu-id="406ad-123">Reliable Services 提供最基本的 API 集合，允許 Service Fabric 執行階段管理服務的生命週期，也允許服務與執行階段互動。</span><span class="sxs-lookup"><span data-stu-id="406ad-123">Reliable Services provide a minimal set of APIs that allow the Service Fabric runtime to manage the lifecycle of your services and that allow your services to interact with the runtime.</span></span> <span data-ttu-id="406ad-124">應用程式架構最為精簡，讓您完整掌控設計和實作選擇，而且可用來裝載任何其他應用程式架構，例如 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="406ad-124">The application framework is minimal, giving you full control over design and implementation choices, and can be used to host any other application framework, such as ASP.NET Core.</span></span>

<span data-ttu-id="406ad-125">Reliable Services 與大多數服務平台 (例如 Web 伺服器) 一樣，可以是無狀態的，其中每個服務執行個體都是以平等方式建立，並且狀態保存在外部解決方案中，例如 Azure DB 或「Azure 資料表儲存體」。</span><span class="sxs-lookup"><span data-stu-id="406ad-125">Reliable Services can be stateless, similar to most service platforms, such as web servers, in which each instance of the service is created equal and state is persisted in an external solution, such as Azure DB or Azure Table Storage.</span></span>

<span data-ttu-id="406ad-126">Reliable Services 也可以是具狀態且為 Service Fabric 專有，其狀態使用 Reliable Collections 直接保存在服務本身中。</span><span class="sxs-lookup"><span data-stu-id="406ad-126">Reliable Services can also be stateful, exclusive to Service Fabric, where state is persisted directly in the service itself using Reliable Collections.</span></span> <span data-ttu-id="406ad-127">狀態透過複寫變得高度可用，並透過資料分割散發，全由 Service Fabric 自動管理。</span><span class="sxs-lookup"><span data-stu-id="406ad-127">State is made highly-available through replication and distributed through partitioning, all managed automatically by Service Fabric.</span></span>

<span data-ttu-id="406ad-128">[深入了解 Reliable Services](service-fabric-reliable-services-introduction.md)或從[撰寫第一個 Reliable Services](service-fabric-reliable-services-quick-start.md) 開始。</span><span class="sxs-lookup"><span data-stu-id="406ad-128">[Learn more about Reliable Services](service-fabric-reliable-services-introduction.md) or get started by [writing your first Reliable Service](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="reliable-actors"></a><span data-ttu-id="406ad-129">Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="406ad-129">Reliable Actors</span></span>
<span data-ttu-id="406ad-130">Reliable Actor 架構是建置在 Reliable Services 最上層的應用程式架構，其根據動作項目設計模式來實作 Virtual Actor 模式。</span><span class="sxs-lookup"><span data-stu-id="406ad-130">Built on top of Reliable Services, the Reliable Actor framework is an application framework that implements the Virtual Actor pattern, based on the actor design pattern.</span></span> <span data-ttu-id="406ad-131">Reliable Actor 架構使用獨立的計算單位，和以單一執行緒方式執行稱為動作項目的狀態。</span><span class="sxs-lookup"><span data-stu-id="406ad-131">The Reliable Actor framework uses independent units of compute and state with single-threaded execution called actors.</span></span> <span data-ttu-id="406ad-132">Reliable Actor 架構提供動作項目的內建通訊和預先設定狀態持續性和相應放大組態。</span><span class="sxs-lookup"><span data-stu-id="406ad-132">The Reliable Actor framework provides built-in communication for actors and pre-set state persistence and scale-out configurations.</span></span>

<span data-ttu-id="406ad-133">Reliable Actors 本身是建置在 Reliable Services 上的應用程式架構，與 Service Fabric 平台完全整合，得益於平台提供的完整功能集。</span><span class="sxs-lookup"><span data-stu-id="406ad-133">As Reliable Actors itself is an application framework built on Reliable Services, it is fully integrated with the Service Fabric platform and benefits from the full set of features offered by the platform.</span></span>

<span data-ttu-id="406ad-134">[深入了解 Reliable Actors](service-fabric-reliable-actors-introduction.md) 或從[撰寫第一項 Reliable Actor 服務](service-fabric-reliable-actors-get-started.md)開始</span><span class="sxs-lookup"><span data-stu-id="406ad-134">[Learn more about Reliable Actors](service-fabric-reliable-actors-introduction.md) or get started by [writing your first Reliable Actor service](service-fabric-reliable-actors-get-started.md)</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="406ad-135">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="406ad-135">ASP.NET Core</span></span>
<span data-ttu-id="406ad-136">Service Fabric 與 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 整合，建置可以是應用程式一部分的 Web 和 API 服務。</span><span class="sxs-lookup"><span data-stu-id="406ad-136">Service Fabric integrates with [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) for building Web and API services that can be included as part of your application.</span></span> 

[<span data-ttu-id="406ad-137">使用 ASP.NET Core 組建前端服務</span><span class="sxs-lookup"><span data-stu-id="406ad-137">Build a front end service using ASP.NET Core</span></span>](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a><span data-ttu-id="406ad-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="406ad-138">Next steps</span></span>
[<span data-ttu-id="406ad-139">Service Fabric 和容器概觀</span><span class="sxs-lookup"><span data-stu-id="406ad-139">Service Fabric and containers overview</span></span>](service-fabric-containers-overview.md)

[<span data-ttu-id="406ad-140">Reliable Services 概觀</span><span class="sxs-lookup"><span data-stu-id="406ad-140">Reliable Services overview</span></span>](service-fabric-reliable-services-introduction.md)

[<span data-ttu-id="406ad-141">Reliable Services 概觀</span><span class="sxs-lookup"><span data-stu-id="406ad-141">Reliable Services overview</span></span>](service-fabric-reliable-actors-introduction.md)

[<span data-ttu-id="406ad-142">Service Fabric 和 ASP.NET Core </span><span class="sxs-lookup"><span data-stu-id="406ad-142">Service Fabric and ASP.NET Core </span></span>](service-fabric-reliable-services-communication-aspnetcore.md)




