---
title: "aaaService 網狀架構程式設計模型概觀 |Microsoft 文件"
description: "Service Fabric 提供這兩個架構來建置服務： hello 動作項目架構並 hello 服務架構。 它們在簡化與控制中提供不同的取捨。"
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
ms.openlocfilehash: b48af2a7b41935bdf0e4594c765f363e520c254e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-programming-model-overview"></a><span data-ttu-id="ef8bd-104">Service Fabric 程式設計模型概觀</span><span class="sxs-lookup"><span data-stu-id="ef8bd-104">Service Fabric programming model overview</span></span>
<span data-ttu-id="ef8bd-105">Service Fabric 提供多個方式 toowrite 並管理您的服務。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-105">Service Fabric offers multiple ways toowrite and manage your services.</span></span> <span data-ttu-id="ef8bd-106">服務可選擇 toouse hello 服務網狀架構 Api tootake 充分善用 hello 平台的功能和應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-106">Services can choose toouse hello Service Fabric APIs tootake full advantage of hello platform's features and application frameworks.</span></span> <span data-ttu-id="ef8bd-107">服務也可以是以任何語言撰寫的任何已編譯可執行程式，或是在 Service Fabric 叢集所裝載之容器中執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-107">Services can also be any compiled executable program written in any language or code running in a container simply hosted on a Service Fabric cluster.</span></span>

## <a name="guest-executables"></a><span data-ttu-id="ef8bd-108">客體可執行檔</span><span class="sxs-lookup"><span data-stu-id="ef8bd-108">Guest executables</span></span>
<span data-ttu-id="ef8bd-109">[客體可執行檔](service-fabric-deploy-existing-app.md)是可在應用程式中作為服務執行的現有任意可執行檔 (以任何語言撰寫)。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-109">A [guest executable](service-fabric-deploy-existing-app.md) is an existing, arbitrary executable (written in any language) that can be run as a service in your application.</span></span> <span data-ttu-id="ef8bd-110">客體可執行檔不直接呼叫 hello Service Fabric SDK Api。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-110">Guest executables do not call hello Service Fabric SDK APIs directly.</span></span> <span data-ttu-id="ef8bd-111">不過他們仍然可以享受功能 hello 平台提供，例如服務探索功能、 自訂健全狀況和報告藉由呼叫 REST Api 服務的網狀架構所公開的負載。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-111">However they still benefit from features hello platform offers, such as service discoverability, custom health and load reporting by calling REST APIs exposed by Service Fabric.</span></span> <span data-ttu-id="ef8bd-112">它們也具備完整的應用程式生命週期支援。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-112">They also have full application lifecycle support.</span></span>

<span data-ttu-id="ef8bd-113">部署您的第一個 [來賓可執行的應用程式](service-fabric-deploy-existing-app.md)，開始使用來賓可執行檔。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-113">Get started with guest executables by deploying your first [guest executable application](service-fabric-deploy-existing-app.md).</span></span>

## <a name="containers"></a><span data-ttu-id="ef8bd-114">容器</span><span class="sxs-lookup"><span data-stu-id="ef8bd-114">Containers</span></span>
<span data-ttu-id="ef8bd-115">根據預設，Service Fabric 會以處理程序形式部署和啟用這些服務。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-115">By default, Service Fabric deploys and activates services as processes.</span></span> <span data-ttu-id="ef8bd-116">Service Fabric 也可以在[容器](service-fabric-containers-overview.md)中部署服務。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-116">Service Fabric can also deploy services in [containers](service-fabric-containers-overview.md).</span></span> <span data-ttu-id="ef8bd-117">Service Fabric 支援在 Windows Server 2016 上部署 Linux 容器和 Windows 容器。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-117">Service Fabric supports deployment of Linux containers and Windows containers on Windows Server 2016.</span></span> <span data-ttu-id="ef8bd-118">可以從任何容器儲存機制提取並部署 toohello 機器容器映像。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-118">Container images can be pulled from any container repository and deployed toohello machine.</span></span> <span data-ttu-id="ef8bd-119">您可以將現有的應用程式部署為來賓 exectuables，Service Fabric 無狀態或狀態可靠的服務或 Reliable Actors 的容器，以及您可以混合使用處理序中的服務和服務中的容器中的 hello 相同的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-119">You can deploy existing applications as guest exectuables, Service Fabric stateless or stateful Reliable services or Reliable Actors in containers, and you can mix services in processes and services in containers in hello same application.</span></span>

[<span data-ttu-id="ef8bd-120">深入了解如何在 Windows 或 Linux 中將服務容器化</span><span class="sxs-lookup"><span data-stu-id="ef8bd-120">Learn more about containerizing your services in Windows or Linux</span></span>](service-fabric-deploy-container.md)

## <a name="reliable-services"></a><span data-ttu-id="ef8bd-121">Reliable Services</span><span class="sxs-lookup"><span data-stu-id="ef8bd-121">Reliable Services</span></span>
<span data-ttu-id="ef8bd-122">可靠的服務是輕量級架構的撰寫與 hello Service Fabric 平台整合，並受益於 hello 組完整的平台功能的服務。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-122">Reliable Services is a light-weight framework for writing services that integrate with hello Service Fabric platform and benefit from hello full set of platform features.</span></span> <span data-ttu-id="ef8bd-123">可靠的服務提供最基本的應用程式開發介面可讓 hello Service Fabric 執行階段 toomanage hello 的生命週期服務，以及可讓您的服務 toointeract hello 執行階段。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-123">Reliable Services provide a minimal set of APIs that allow hello Service Fabric runtime toomanage hello lifecycle of your services and that allow your services toointeract with hello runtime.</span></span> <span data-ttu-id="ef8bd-124">是最小的 hello 應用程式架構，讓您完整控制設計和實作的選項，而且可以使用的 toohost 任何其他應用程式架構，例如 ASP.NET Core。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-124">hello application framework is minimal, giving you full control over design and implementation choices, and can be used toohost any other application framework, such as ASP.NET Core.</span></span>

<span data-ttu-id="ef8bd-125">可靠的服務可以是無狀態，類似 toomost 服務平台，例如 web 伺服器，在其中均等建立 hello 服務的每個執行個體和狀態會持續保留在外部的解決方案，例如 Azure DB 或 Azure 資料表儲存體。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-125">Reliable Services can be stateless, similar toomost service platforms, such as web servers, in which each instance of hello service is created equal and state is persisted in an external solution, such as Azure DB or Azure Table Storage.</span></span>

<span data-ttu-id="ef8bd-126">可靠的服務也可以是可設定狀態、 獨佔 tooService 網狀架構，其中保存直接在 hello 服務本身使用可靠的集合中的狀態。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-126">Reliable Services can also be stateful, exclusive tooService Fabric, where state is persisted directly in hello service itself using Reliable Collections.</span></span> <span data-ttu-id="ef8bd-127">狀態透過複寫變得高度可用，並透過資料分割散發，全由 Service Fabric 自動管理。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-127">State is made highly-available through replication and distributed through partitioning, all managed automatically by Service Fabric.</span></span>

<span data-ttu-id="ef8bd-128">[深入了解 Reliable Services](service-fabric-reliable-services-introduction.md)或從[撰寫第一個 Reliable Services](service-fabric-reliable-services-quick-start.md) 開始。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-128">[Learn more about Reliable Services](service-fabric-reliable-services-introduction.md) or get started by [writing your first Reliable Service](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="reliable-actors"></a><span data-ttu-id="ef8bd-129">Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ef8bd-129">Reliable Actors</span></span>
<span data-ttu-id="ef8bd-130">Hello Reliable Actor 架構之上可靠的服務，是一種應用程式架構，以實作 hello Virtual Actor 模式，根據 hello 執行者設計模式。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-130">Built on top of Reliable Services, hello Reliable Actor framework is an application framework that implements hello Virtual Actor pattern, based on hello actor design pattern.</span></span> <span data-ttu-id="ef8bd-131">hello Reliable Actor framework 會使用稱為執行者的單一執行緒執行獨立的單位計算和狀態。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-131">hello Reliable Actor framework uses independent units of compute and state with single-threaded execution called actors.</span></span> <span data-ttu-id="ef8bd-132">hello Reliable Actor 架構提供執行者與預先設定的狀態持續性和向外延展設定的內建的通訊。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-132">hello Reliable Actor framework provides built-in communication for actors and pre-set state persistence and scale-out configurations.</span></span>

<span data-ttu-id="ef8bd-133">Reliable Actors 本身是建置在可靠的服務應用程式架構，因為它會完全整合 hello Service Fabric 平台與 hello hello 平台所提供的功能的一組完整的利益。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-133">As Reliable Actors itself is an application framework built on Reliable Services, it is fully integrated with hello Service Fabric platform and benefits from hello full set of features offered by hello platform.</span></span>

<span data-ttu-id="ef8bd-134">[深入了解 Reliable Actors](service-fabric-reliable-actors-introduction.md) 或從[撰寫第一項 Reliable Actor 服務](service-fabric-reliable-actors-get-started.md)開始</span><span class="sxs-lookup"><span data-stu-id="ef8bd-134">[Learn more about Reliable Actors](service-fabric-reliable-actors-introduction.md) or get started by [writing your first Reliable Actor service](service-fabric-reliable-actors-get-started.md)</span></span>

## <a name="aspnet-core"></a><span data-ttu-id="ef8bd-135">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="ef8bd-135">ASP.NET Core</span></span>
<span data-ttu-id="ef8bd-136">Service Fabric 與 [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) 整合，建置可以是應用程式一部分的 Web 和 API 服務。</span><span class="sxs-lookup"><span data-stu-id="ef8bd-136">Service Fabric integrates with [ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) for building Web and API services that can be included as part of your application.</span></span> 

[<span data-ttu-id="ef8bd-137">使用 ASP.NET Core 組建前端服務</span><span class="sxs-lookup"><span data-stu-id="ef8bd-137">Build a front end service using ASP.NET Core</span></span>](service-fabric-add-a-web-frontend.md)

## <a name="next-steps"></a><span data-ttu-id="ef8bd-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ef8bd-138">Next steps</span></span>
[<span data-ttu-id="ef8bd-139">Service Fabric 和容器概觀</span><span class="sxs-lookup"><span data-stu-id="ef8bd-139">Service Fabric and containers overview</span></span>](service-fabric-containers-overview.md)

[<span data-ttu-id="ef8bd-140">Reliable Services 概觀</span><span class="sxs-lookup"><span data-stu-id="ef8bd-140">Reliable Services overview</span></span>](service-fabric-reliable-services-introduction.md)

[<span data-ttu-id="ef8bd-141">Reliable Services 概觀</span><span class="sxs-lookup"><span data-stu-id="ef8bd-141">Reliable Services overview</span></span>](service-fabric-reliable-actors-introduction.md)

[<span data-ttu-id="ef8bd-142">Service Fabric 和 ASP.NET Core </span><span class="sxs-lookup"><span data-stu-id="ef8bd-142">Service Fabric and ASP.NET Core </span></span>](service-fabric-reliable-services-communication-aspnetcore.md)




