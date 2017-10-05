---
title: "Azure Service Fabric 模式和案例 | Microsoft Docs"
description: "了解最佳作法，並證明可重複使用的模式來設計、開發及操作您的微服務，Service Fabric 上。"
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
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="53ea8-103">Service Fabric 模式和案例</span><span class="sxs-lookup"><span data-stu-id="53ea8-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="53ea8-104">如果您正在觀看如何使用 Azure Service Fabric 建置大規模微服務，請向負責設計及建置此平台即服務 (PaaS) 的專家學習。</span><span class="sxs-lookup"><span data-stu-id="53ea8-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="53ea8-105">從適當的架構開始，接著了解如何將您應用程式的資源最佳化。</span><span class="sxs-lookup"><span data-stu-id="53ea8-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="53ea8-106">[Service Fabric 模式和實務](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344)課程會回答真實客戶最常詢問的 Service Fabric 案例和應用程式領域相關問題。</span><span class="sxs-lookup"><span data-stu-id="53ea8-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="53ea8-107">了解如何使用最佳作法和經過實證且可重複使用的模式，在 Service Fabric 上設計、開發及操作您的微服務。</span><span class="sxs-lookup"><span data-stu-id="53ea8-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="53ea8-108">取得 Service Fabric 的概觀，然後深入了解涵蓋叢集最佳化和安全性、移轉舊版應用程式、大規模 IoT、裝載遊戲引擎等的主題。</span><span class="sxs-lookup"><span data-stu-id="53ea8-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="53ea8-109">查看各種工作負載的連續傳遞，甚至取得 Linux 支援和容器的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="53ea8-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="53ea8-110">簡介</span><span class="sxs-lookup"><span data-stu-id="53ea8-110">Introduction</span></span>
<span data-ttu-id="53ea8-111">瀏覽最佳作法，並了解為何選擇平台即服務 (PaaS) 而不是基礎結構即服務 (IaaS)。</span><span class="sxs-lookup"><span data-stu-id="53ea8-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="53ea8-112">取得下列已經實證之應用程式設計原則的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="53ea8-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="53ea8-113">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-113">Video</span></span></th><th><span data-ttu-id="53ea8-114">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Service Fabric 簡介</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="53ea8-116">叢集規劃與管理</span><span class="sxs-lookup"><span data-stu-id="53ea8-116">Cluster planning and management</span></span>
<span data-ttu-id="53ea8-117">觀看此處的 Azure Service Fabric，了解容量規劃、叢集最佳化和叢集安全性。</span><span class="sxs-lookup"><span data-stu-id="53ea8-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="53ea8-118">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-118">Video</span></span></th><th><span data-ttu-id="53ea8-119">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="53ea8-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">叢集規劃與管理</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="53ea8-121">超大規模 Web</span><span class="sxs-lookup"><span data-stu-id="53ea8-121">Hyper-scale web</span></span>
<span data-ttu-id="53ea8-122">檢閱超大規模 Web 的概念，包括可用性和可靠性、超規模以及狀態管理。</span><span class="sxs-lookup"><span data-stu-id="53ea8-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="53ea8-123">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-123">Video</span></span></th><th><span data-ttu-id="53ea8-124">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">超大規模 Web</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="53ea8-126">IoT</span><span class="sxs-lookup"><span data-stu-id="53ea8-126">IoT</span></span>
<span data-ttu-id="53ea8-127">探索 Azure Service Fabric 環境中的物聯網 (IoT)，包括 Azure IoT 管線、多重租用和大規模 IoT。</span><span class="sxs-lookup"><span data-stu-id="53ea8-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="53ea8-128">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-128">Video</span></span></th><th><span data-ttu-id="53ea8-129">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="53ea8-131">玩遊戲</span><span class="sxs-lookup"><span data-stu-id="53ea8-131">Gaming</span></span>
<span data-ttu-id="53ea8-132">察看回合制遊戲、互動式遊戲，以及裝載現有的遊戲引擎。</span><span class="sxs-lookup"><span data-stu-id="53ea8-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="53ea8-133">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-133">Video</span></span></th><th><span data-ttu-id="53ea8-134">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">遊戲</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="53ea8-136">持續傳遞</span><span class="sxs-lookup"><span data-stu-id="53ea8-136">Continuous delivery</span></span>
<span data-ttu-id="53ea8-137">探索相關概念，包括使用 Visual Studio Team Services、建置/封裝/發佈工作流程、多重環境設定及服務套件/共用的連續整合/連續傳遞。</span><span class="sxs-lookup"><span data-stu-id="53ea8-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="53ea8-138">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-138">Video</span></span></th><th><span data-ttu-id="53ea8-139">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">持續傳遞</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="53ea8-141">移轉</span><span class="sxs-lookup"><span data-stu-id="53ea8-141">Migration</span></span>
<span data-ttu-id="53ea8-142">除了舊版應用程式的移轉以外，還要了解如何從雲端服務移轉。</span><span class="sxs-lookup"><span data-stu-id="53ea8-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="53ea8-143">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-143">Video</span></span></th><th><span data-ttu-id="53ea8-144">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">移轉</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="53ea8-146">容器和 Linux 支援</span><span class="sxs-lookup"><span data-stu-id="53ea8-146">Containers and Linux support</span></span>
<span data-ttu-id="53ea8-147">取得「為何使用容器？」問題的答案</span><span class="sxs-lookup"><span data-stu-id="53ea8-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="53ea8-148">了解 Windows 容器、Linux 支援和 Linux 容器協調流程的概況簡介。</span><span class="sxs-lookup"><span data-stu-id="53ea8-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="53ea8-149">此外，了解如何將 .NET Core 應用程式移轉至 Linux。</span><span class="sxs-lookup"><span data-stu-id="53ea8-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="53ea8-150">影片</span><span class="sxs-lookup"><span data-stu-id="53ea8-150">Video</span></span></th><th><span data-ttu-id="53ea8-151">PowerPoint 簡報</span><span class="sxs-lookup"><span data-stu-id="53ea8-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="53ea8-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">容器和 Linux 支援</a></span><span class="sxs-lookup"><span data-stu-id="53ea8-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="53ea8-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53ea8-153">Next steps</span></span>
<span data-ttu-id="53ea8-154">既然您已了解 Service Fabric 模式和案例，請深入了解如何[建立和管理叢集](service-fabric-deploy-anywhere.md)、[將雲端服務應用程式移轉至 Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md)、[設定連續傳遞](service-fabric-set-up-continuous-integration.md)以及[部署容器](service-fabric-containers-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="53ea8-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
