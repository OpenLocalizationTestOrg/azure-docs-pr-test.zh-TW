---
title: "Linux 上的 Azure Service Fabric | Microsoft Docs"
description: "Service Fabric 叢集支援 Linux 和 Java，這表示您能夠在 Linux 上部署和裝載以 Java 和 C# 撰寫的 Service Fabric 應用程式。"
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 459afade-145d-4ee6-b72b-ddf380ccd1bf
ms.service: service-fabric
ms.devlang: Java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: SubramaR
ms.openlocfilehash: dddc9f698d9776999d406117b46285a0f90d9620
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="241e1-103">Linux 上的 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="241e1-103">Service Fabric on Linux</span></span>
<span data-ttu-id="241e1-104">Linux 上的 Service Fabric 預覽版可讓您如同在 Windows 上一樣，在 Linux 上建置、部署和管理高可用性、可高度調整的應用程式。</span><span class="sxs-lookup"><span data-stu-id="241e1-104">The preview of Service Fabric on Linux enables you to build, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="241e1-105">Service Fabric 架構 (Reliable Services 和 Reliable Actors) 除了可在 C# (.NET Core) 中使用，也能在 Java on Linux 中使用。</span><span class="sxs-lookup"><span data-stu-id="241e1-105">The Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition to C# (.NET Core).</span></span>  <span data-ttu-id="241e1-106">您也可以使用任何語言或架構來建置 [來賓可執行檔服務](service-fabric-deploy-existing-app.md) 。</span><span class="sxs-lookup"><span data-stu-id="241e1-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="241e1-107">此外，預覽也支援協調 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="241e1-107">In addition, the preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="241e1-108">Docker 容器可以執行使用 Service Fabric 架構的來賓可執行檔或原生 Service Fabric 服務。</span><span class="sxs-lookup"><span data-stu-id="241e1-108">Docker containers can run guest executables or native Service Fabric services, which use the Service Fabric frameworks.</span></span>

<span data-ttu-id="241e1-109">Linux 上的 Service Fabric 在概念上相當於 Windows 上的 Service Fabric (除了作業系統細節和程式設計語言支援)。</span><span class="sxs-lookup"><span data-stu-id="241e1-109">Service Fabric on Linux is conceptually equivalent to Service Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="241e1-110">因此，我們大部分的 [現有文件](http://aka.ms/servicefabricdocs) 都可協助您熟悉這項技術。</span><span class="sxs-lookup"><span data-stu-id="241e1-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with the technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="241e1-111">支援的作業系統和程式設計語言</span><span class="sxs-lookup"><span data-stu-id="241e1-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="241e1-112">有限預覽版除了支援在 Azure 中執行 Ubuntu Server 16.04 的多部電腦叢集，還支援建立一整體開發叢集。</span><span class="sxs-lookup"><span data-stu-id="241e1-112">The limited preview supports the creation of one-box development clusters in addition to multi-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="241e1-113">除了來賓可執行檔和協調 Docker 容器，預覽在 Java 和 C# 中還支援 Reliable Actors 和 Reliable Stateless Services 架構。</span><span class="sxs-lookup"><span data-stu-id="241e1-113">The preview supports the Reliable Actors and the Reliable Stateless Services frameworks in Java and C# in addition to guest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="241e1-114">Linux 尚未支援 Reliable Collections。</span><span class="sxs-lookup"><span data-stu-id="241e1-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="241e1-115">也不支援獨立叢集 - 預覽中僅支援單機和 Azure Linux 多電腦叢集。</span><span class="sxs-lookup"><span data-stu-id="241e1-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in the preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="241e1-116">支援的工具</span><span class="sxs-lookup"><span data-stu-id="241e1-116">Supported tooling</span></span>
<span data-ttu-id="241e1-117">預覽支援透過 Service Fabric CLI 來與叢集進行互動。</span><span class="sxs-lookup"><span data-stu-id="241e1-117">The preview supports interaction with the cluster through Service Fabric CLI.</span></span> <span data-ttu-id="241e1-118">針對 Java 開發人員，透過 Linux 和 OSX 上支援的 Eclipse，就能與 Eclipse 和 Yeoman 整合。</span><span class="sxs-lookup"><span data-stu-id="241e1-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="241e1-119">OSX 整合透過 vagrant 在幕後使用 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="241e1-119">The OSX integration uses a Linux VM under the hood via vagrant.</span></span> <span data-ttu-id="241e1-120">針對 C# 開發人員，支援與 Yeoman 整合來產生應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="241e1-120">For C# developers, integration with Yeoman is provided to generate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="241e1-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="241e1-121">Next steps</span></span>

* <span data-ttu-id="241e1-122">請熟悉 [Reliable Actors](service-fabric-reliable-actors-introduction.md) 和 [Reliable Services](service-fabric-reliable-services-introduction.md) 程式設計架構</span><span class="sxs-lookup"><span data-stu-id="241e1-122">Get familiar with the [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="241e1-123">在 Linux 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="241e1-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="241e1-124">在 OSX 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="241e1-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="241e1-125">在 Linux 上建立第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="241e1-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="241e1-126">使用 Jenkins 和 GitHub 設定 Service Fabric 連續整合和部署</span><span class="sxs-lookup"><span data-stu-id="241e1-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="241e1-127">Service Fabric Windows/Linux 的差異</span><span class="sxs-lookup"><span data-stu-id="241e1-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
