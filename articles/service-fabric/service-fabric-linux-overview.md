---
title: "在 Linux 上的 Service Fabric aaaAzure |Microsoft 文件"
description: "Service Fabric 叢集支援 Linux 和 Java 中，這表示您將會無法 toodeploy 而且 Java 和 C# 中撰寫在 Linux 上的主機 Service Fabric 應用程式。"
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
ms.openlocfilehash: ca0e092b00faec560963c0d6cc379593d085f6a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-on-linux"></a><span data-ttu-id="4ee05-103">Linux 上的 Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4ee05-103">Service Fabric on Linux</span></span>
<span data-ttu-id="4ee05-104">在 Linux 上的 Service Fabric hello 預覽可讓您 toobuild、 部署和管理 Linux 上的高可用性、 高擴充性應用程式，就如同在 Windows 上。</span><span class="sxs-lookup"><span data-stu-id="4ee05-104">hello preview of Service Fabric on Linux enables you toobuild, deploy, and manage highly available, highly scalable applications on Linux just as you would on Windows.</span></span> <span data-ttu-id="4ee05-105">在 Linux 上的 Java 加法 tooC # (.NET Core) 中使用 hello Service Fabric 架構 （可靠的服務和 Reliable Actors）。</span><span class="sxs-lookup"><span data-stu-id="4ee05-105">hello Service Fabric frameworks (Reliable Services and Reliable Actors) are available in Java on Linux in addition tooC# (.NET Core).</span></span>  <span data-ttu-id="4ee05-106">您也可以使用任何語言或架構來建置 [來賓可執行檔服務](service-fabric-deploy-existing-app.md) 。</span><span class="sxs-lookup"><span data-stu-id="4ee05-106">You can also build [guest executable services](service-fabric-deploy-existing-app.md) with any language or framework.</span></span> <span data-ttu-id="4ee05-107">此外，hello 預覽也支援協調 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="4ee05-107">In addition, hello preview also supports orchestrating Docker containers.</span></span> <span data-ttu-id="4ee05-108">客體可執行檔或原生的 Service Fabric 服務，使用 hello Service Fabric 架構，可以執行 docker 容器。</span><span class="sxs-lookup"><span data-stu-id="4ee05-108">Docker containers can run guest executables or native Service Fabric services, which use hello Service Fabric frameworks.</span></span>

<span data-ttu-id="4ee05-109">在 Linux 上的 Service Fabric 這概念上相當 tooService Windows 上的網狀架構 （除了作業系統特性和程式設計語言支援）。</span><span class="sxs-lookup"><span data-stu-id="4ee05-109">Service Fabric on Linux is conceptually equivalent tooService Fabric on Windows (except for OS specifics and programming language support).</span></span> <span data-ttu-id="4ee05-110">因此，大部分的我們[現有文件集](http://aka.ms/servicefabricdocs)適用於協助您熟悉 hello 技術。</span><span class="sxs-lookup"><span data-stu-id="4ee05-110">Thus, most of our [existing documentation](http://aka.ms/servicefabricdocs) applies in helping you get familiar with hello technology.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Service-Fabric-Linux-Preview/player]
>
>

## <a name="supported-operating-systems-and-programming-languages"></a><span data-ttu-id="4ee05-111">支援的作業系統和程式設計語言</span><span class="sxs-lookup"><span data-stu-id="4ee05-111">Supported operating systems and programming languages</span></span>
<span data-ttu-id="4ee05-112">有限的 hello 預覽支援 hello 建立一個方塊開發此外叢集在 Azure 中執行 Ubuntu Server 16.04 toomulti 機器叢集。</span><span class="sxs-lookup"><span data-stu-id="4ee05-112">hello limited preview supports hello creation of one-box development clusters in addition toomulti-machine clusters in Azure running Ubuntu Server 16.04.</span></span> <span data-ttu-id="4ee05-113">hello 預覽支援 hello Reliable Actors 和 hello Java 和 C# 中的可靠的無狀態服務架構新增 tooguest 可執行檔和協調 Docker 容器中。</span><span class="sxs-lookup"><span data-stu-id="4ee05-113">hello preview supports hello Reliable Actors and hello Reliable Stateless Services frameworks in Java and C# in addition tooguest executables and orchestrating Docker containers.</span></span>  

> [!NOTE]
> <span data-ttu-id="4ee05-114">Linux 尚未支援 Reliable Collections。</span><span class="sxs-lookup"><span data-stu-id="4ee05-114">Reliable Collections are not supported in Linux yet.</span></span> <span data-ttu-id="4ee05-115">不支援獨立單獨叢集 hello 預覽支援是-只有一個方塊和 Azure Linux 多電腦叢集。</span><span class="sxs-lookup"><span data-stu-id="4ee05-115">Stand alone clusters aren't supported either - only one box and Azure Linux multi-machine clusters are supported in hello preview.</span></span>
>
>


## <a name="supported-tooling"></a><span data-ttu-id="4ee05-116">支援的工具</span><span class="sxs-lookup"><span data-stu-id="4ee05-116">Supported tooling</span></span>
<span data-ttu-id="4ee05-117">hello 預覽支援與透過 Service Fabric CLI hello 叢集之間的互動。</span><span class="sxs-lookup"><span data-stu-id="4ee05-117">hello preview supports interaction with hello cluster through Service Fabric CLI.</span></span> <span data-ttu-id="4ee05-118">針對 Java 開發人員，透過 Linux 和 OSX 上支援的 Eclipse，就能與 Eclipse 和 Yeoman 整合。</span><span class="sxs-lookup"><span data-stu-id="4ee05-118">For Java developers, integration with Eclipse and Yeoman is provided with Eclipse supported on Linux and on OSX.</span></span> <span data-ttu-id="4ee05-119">hello OSX 整合會使用透過 vagrant hello 幕後 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="4ee05-119">hello OSX integration uses a Linux VM under hello hood via vagrant.</span></span> <span data-ttu-id="4ee05-120">C# 開發人員，與 Yeoman 整合提供 toogenerate 應用程式範本。</span><span class="sxs-lookup"><span data-stu-id="4ee05-120">For C# developers, integration with Yeoman is provided toogenerate application templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ee05-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ee05-121">Next steps</span></span>

* <span data-ttu-id="4ee05-122">讓您熟悉 hello [Reliable Actors](service-fabric-reliable-actors-introduction.md)和[可靠服務](service-fabric-reliable-services-introduction.md)程式設計架構</span><span class="sxs-lookup"><span data-stu-id="4ee05-122">Get familiar with hello [Reliable Actors](service-fabric-reliable-actors-introduction.md) and [Reliable Services](service-fabric-reliable-services-introduction.md) programming frameworks</span></span>
* [<span data-ttu-id="4ee05-123">在 Linux 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="4ee05-123">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="4ee05-124">在 OSX 上準備您的開發環境</span><span class="sxs-lookup"><span data-stu-id="4ee05-124">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="4ee05-125">在 Linux 上建立第一個 Service Fabric Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="4ee05-125">Create your first Service Fabric Java application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="4ee05-126">使用 Jenkins 和 GitHub 設定 Service Fabric 連續整合和部署</span><span class="sxs-lookup"><span data-stu-id="4ee05-126">Setup Service Fabric continuous integration and deployment with Jenkins and GitHub</span></span>](service-fabric-cicd-your-linux-java-application-with-jenkins.md)
* [<span data-ttu-id="4ee05-127">Service Fabric Windows/Linux 的差異</span><span class="sxs-lookup"><span data-stu-id="4ee05-127">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
