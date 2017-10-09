---
title: "Service Fabric aaaAzure 模式和案例 |Microsoft 文件"
description: "了解最佳作法，並證明，可重複使用的模式 toodesign 開發及操作您 microservices 服務網狀架構上。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="c1650-103">Service Fabric 模式和案例</span><span class="sxs-lookup"><span data-stu-id="c1650-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="c1650-104">如果您要尋找在建置大型 microservices 使用 Azure Service Fabric，了解設計和建置此平台即服務 (PaaS) hello 專家。</span><span class="sxs-lookup"><span data-stu-id="c1650-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="c1650-105">開始使用適當的架構，然後了解如何 toooptimize 資源應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1650-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="c1650-106">hello[服務網狀架構 Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344)課程回答 hello 問題最常詢問真實世界的客戶服務網狀架構案例和應用程式區域。</span><span class="sxs-lookup"><span data-stu-id="c1650-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="c1650-107">了解如何 toodesign，開發，以及操作您 microservices 上服務的網狀架構使用的最佳作法和經過驗證、 可重複使用的模式。</span><span class="sxs-lookup"><span data-stu-id="c1650-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="c1650-108">取得 Service Fabric 的概觀，然後深入了解涵蓋叢集最佳化和安全性、移轉舊版應用程式、大規模 IoT、裝載遊戲引擎等的主題。</span><span class="sxs-lookup"><span data-stu-id="c1650-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="c1650-109">查閱持續傳遞不同的工作負載，並取得 hello Linux 支援和容器的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c1650-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="c1650-110">簡介</span><span class="sxs-lookup"><span data-stu-id="c1650-110">Introduction</span></span>
<span data-ttu-id="c1650-111">瀏覽最佳作法，並了解為何選擇平台即服務 (PaaS) 而不是基礎結構即服務 (IaaS)。</span><span class="sxs-lookup"><span data-stu-id="c1650-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="c1650-112">在下列經過證實的應用程式設計原則取得 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c1650-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="c1650-113">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-113">Video</span></span></th><th><span data-ttu-id="c1650-114">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">簡介 tooService 網狀架構</a></span><span class="sxs-lookup"><span data-stu-id="c1650-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="c1650-116">叢集規劃與管理</span><span class="sxs-lookup"><span data-stu-id="c1650-116">Cluster planning and management</span></span>
<span data-ttu-id="c1650-117">觀看此處的 Azure Service Fabric，了解容量規劃、叢集最佳化和叢集安全性。</span><span class="sxs-lookup"><span data-stu-id="c1650-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="c1650-118">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-118">Video</span></span></th><th><span data-ttu-id="c1650-119">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="c1650-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">叢集規劃與管理</a></span><span class="sxs-lookup"><span data-stu-id="c1650-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="c1650-121">超大規模 Web</span><span class="sxs-lookup"><span data-stu-id="c1650-121">Hyper-scale web</span></span>
<span data-ttu-id="c1650-122">檢閱超大規模 Web 的概念，包括可用性和可靠性、超規模以及狀態管理。</span><span class="sxs-lookup"><span data-stu-id="c1650-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="c1650-123">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-123">Video</span></span></th><th><span data-ttu-id="c1650-124">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">超大規模 Web</a></span><span class="sxs-lookup"><span data-stu-id="c1650-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="c1650-126">IoT</span><span class="sxs-lookup"><span data-stu-id="c1650-126">IoT</span></span>
<span data-ttu-id="c1650-127">Azure Service Fabric，包括 hello Azure IoT 管線、 多租用戶和 IoT 大規模 hello 內容中，瀏覽 hello 物聯網 (IoT)。</span><span class="sxs-lookup"><span data-stu-id="c1650-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="c1650-128">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-128">Video</span></span></th><th><span data-ttu-id="c1650-129">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="c1650-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="c1650-131">玩遊戲</span><span class="sxs-lookup"><span data-stu-id="c1650-131">Gaming</span></span>
<span data-ttu-id="c1650-132">察看回合制遊戲、互動式遊戲，以及裝載現有的遊戲引擎。</span><span class="sxs-lookup"><span data-stu-id="c1650-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="c1650-133">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-133">Video</span></span></th><th><span data-ttu-id="c1650-134">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">遊戲</a></span><span class="sxs-lookup"><span data-stu-id="c1650-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="c1650-136">持續傳遞</span><span class="sxs-lookup"><span data-stu-id="c1650-136">Continuous delivery</span></span>
<span data-ttu-id="c1650-137">探索相關概念，包括使用 Visual Studio Team Services、建置/封裝/發佈工作流程、多重環境設定及服務套件/共用的連續整合/連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="c1650-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="c1650-138">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-138">Video</span></span></th><th><span data-ttu-id="c1650-139">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">持續傳遞</a></span><span class="sxs-lookup"><span data-stu-id="c1650-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="c1650-141">移轉</span><span class="sxs-lookup"><span data-stu-id="c1650-141">Migration</span></span>
<span data-ttu-id="c1650-142">深入了解從移轉的雲端服務，除了 toomigration 的舊版應用程式。</span><span class="sxs-lookup"><span data-stu-id="c1650-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="c1650-143">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-143">Video</span></span></th><th><span data-ttu-id="c1650-144">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">移轉</a></span><span class="sxs-lookup"><span data-stu-id="c1650-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="c1650-146">容器和 Linux 支援</span><span class="sxs-lookup"><span data-stu-id="c1650-146">Containers and Linux support</span></span>
<span data-ttu-id="c1650-147">取得 hello 回應 toohello 問題時，「 為什麼容器嗎？ 」</span><span class="sxs-lookup"><span data-stu-id="c1650-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="c1650-148">深入了解 Windows 容器、 Linux 支援和 Linux 容器協調流程的 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="c1650-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="c1650-149">此外，了解如何 toomigrate.NET Core 應用程式 tooLinux。</span><span class="sxs-lookup"><span data-stu-id="c1650-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="c1650-150">影片</span><span class="sxs-lookup"><span data-stu-id="c1650-150">Video</span></span></th><th><span data-ttu-id="c1650-151">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="c1650-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="c1650-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">容器和 Linux 支援</a></span><span class="sxs-lookup"><span data-stu-id="c1650-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="c1650-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1650-153">Next steps</span></span>
<span data-ttu-id="c1650-154">既然您已了解 Service Fabric 模式和案例，深入了解如何太[建立和管理叢集](service-fabric-deploy-anywhere.md)，[移轉雲端服務應用程式 tooService 網狀架構](service-fabric-cloud-services-migration-worker-role-stateless-service.md)，[設定持續傳遞](service-fabric-set-up-continuous-integration.md)，和[部署容器](service-fabric-containers-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c1650-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
