---
title: "在 Azure 中的 aaaPrivate Docker 容器登錄 |Microsoft 文件"
description: "簡介 toohello Azure 容器登錄 服務，提供雲端式管理的私人 Docker 登錄。"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a><span data-ttu-id="a1ca7-103">簡介 tooprivate Docker 容器登錄</span><span class="sxs-lookup"><span data-stu-id="a1ca7-103">Introduction tooprivate Docker container registries</span></span>


<span data-ttu-id="a1ca7-104">Azure 容器登錄中是 managed [Docker 登錄](https://docs.docker.com/registry/)根據服務 hello 開放原始碼 Docker 登錄 2.0。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-104">Azure Container Registry is a managed [Docker registry](https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="a1ca7-105">建立和維護 Azure 容器登錄 toostore 和管理您的私人[Docker 容器](https://www.docker.com/what-docker)映像。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-105">Create and maintain Azure container registries toostore and manage your private [Docker container](https://www.docker.com/what-docker) images.</span></span> <span data-ttu-id="a1ca7-106">容器登錄在 Azure 中的使用現有的容器開發與部署管線和 Docker 社群專業知識的 hello 主體上繪製。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-106">Use container registries in Azure with your existing container development and deployment pipelines, and draw on hello body of Docker community expertise.</span></span>

<span data-ttu-id="a1ca7-107">如需有關 Docker 和容器的背景，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="a1ca7-107">For background about Docker and containers, see:</span></span>

* [<span data-ttu-id="a1ca7-108">Docker 使用者指南</span><span class="sxs-lookup"><span data-stu-id="a1ca7-108">Docker user guide</span></span>](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a><span data-ttu-id="a1ca7-109">使用案例</span><span class="sxs-lookup"><span data-stu-id="a1ca7-109">Use cases</span></span>
<span data-ttu-id="a1ca7-110">提取映像從 Azure 容器登錄 toovarious 部署目標：</span><span class="sxs-lookup"><span data-stu-id="a1ca7-110">Pull images from an Azure container registry toovarious deployment targets:</span></span>

* <span data-ttu-id="a1ca7-111">**可調整的協調流程系統**，會管理整個主機叢集上容器化的應用程式，包括 [DC/OS](https://docs.mesosphere.com/)、[Docker Swarm](https://docs.docker.com/swarm/)、 [Kubernetes](http://kubernetes.io/docs/)。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-111">**Scalable orchestration systems** that manage containerized applications across clusters of hosts, including [DC/OS](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/), and [Kubernetes](http://kubernetes.io/docs/).</span></span>
* <span data-ttu-id="a1ca7-112">**Azure 服務**，會支援依規模建置和執行的應用程式，包括 [Container Service](../container-service/index.yml)、[App Service](/app-service/index.md)、[Batch](../batch/index.md)、[Service Fabric](/azure/service-fabric/) 和其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-112">**Azure services** that support building and running applications at scale, including [Container Service](../container-service/index.yml), [App Service](/app-service/index.md), [Batch](../batch/index.md), [Service Fabric](/azure/service-fabric/), and others.</span></span>

<span data-ttu-id="a1ca7-113">開發人員也可以推送 tooa 容器登錄中做為容器的開發工作流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-113">Developers can also push tooa container registry as part of a container development workflow.</span></span> <span data-ttu-id="a1ca7-114">例如，以容器登錄庫為目標，並以 [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) 或 [Jenkins](https://jenkins.io/) 等持續整合與部署工具為起點。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-114">For example, target a container registry from a continuous integration and deployment tool such as [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) or [Jenkins](https://jenkins.io/).</span></span>





## <a name="key-concepts"></a><span data-ttu-id="a1ca7-115">重要概念</span><span class="sxs-lookup"><span data-stu-id="a1ca7-115">Key concepts</span></span>
* <span data-ttu-id="a1ca7-116">**登錄庫** - 在您的 Azure 訂用帳戶中建立一或多個容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-116">**Registry** - Create one or more container registries in your Azure subscription.</span></span> <span data-ttu-id="a1ca7-117">每個登錄支援標準 Azure[儲存體帳戶](../storage/common/storage-introduction.md)hello 中相同的位置。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-117">Each registry is backed by a standard Azure [storage account](../storage/common/storage-introduction.md) in hello same location.</span></span> <span data-ttu-id="a1ca7-118">利用本機、 網路關閉您的容器映像的儲存體藉由建立登錄在 hello 與您的部署相同的 Azure 位置。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-118">Take advantage of local, network-close storage of your container images by creating a registry in hello same Azure location as your deployments.</span></span> <span data-ttu-id="a1ca7-119">完整的登錄名稱具有 hello 表單`myregistry.azurecr.io`。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-119">A fully qualified registry name has hello form `myregistry.azurecr.io`.</span></span>

  <span data-ttu-id="a1ca7-120">您[控制存取](container-registry-authentication.md)tooa 容器登錄中使用 Azure Active Directory 備份[服務主體](../active-directory/active-directory-application-objects.md)或提供的系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-120">You [control access](container-registry-authentication.md) tooa container registry using an Azure Active Directory-backed [service principal](../active-directory/active-directory-application-objects.md) or a provided admin account.</span></span> <span data-ttu-id="a1ca7-121">執行標準的 hello`docker login`命令 tooauthenticate 登錄。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-121">Run hello standard `docker login` command tooauthenticate with a registry.</span></span>

* <span data-ttu-id="a1ca7-122">**受管理登錄** - 為三個 SKU 中的登錄提供額外功能的層級 - 基本、標準和進階。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-122">**Managed Registry** - A tier that offers additional capabilities for registries in three SKUs - Basic, Standard, and Premium.</span></span> <span data-ttu-id="a1ca7-123">在這些 Sku 的 hello 影像會儲存在 hello Azure 容器登錄服務，因此可提高可靠性，並啟用新功能所管理的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-123">hello images in these SKUs are stored in Storage Accounts managed by hello Azure Container Registries service, which improves reliability and enables new features.</span></span> <span data-ttu-id="a1ca7-124">新功能包括 Webhook 整合、與 Azure Active Directory 的存放庫驗證，以及刪除功能支援。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-124">New capabilities include webhook integration, repository authentication with Azure Active Directory, and support for delete functionality.</span></span> <span data-ttu-id="a1ca7-125">使用者擁有 hello 選項 toochoose managed 的登錄或 toocreate 之間建立登錄時，他們自己的儲存體帳戶所支援的登錄。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-125">Users have hello option toochoose between managed registries or toocreate a registry backed by their own Storage Accounts when creating registries.</span></span>

* <span data-ttu-id="a1ca7-126">**儲存機制** - 登錄庫會包含一個或多個儲存機制，儲存機制是容器映像的群組。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-126">**Repository** - A registry contains one or more repositories, which are groups of container images.</span></span> <span data-ttu-id="a1ca7-127">Azure 容器登錄庫支援多層級的儲存機制命名空間。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-127">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="a1ca7-128">這項功能可讓您 toogroup 集合的映像相關的 tooa 特定應用程式或應用程式 toospecific 開發或操作團隊的集合。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-128">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="a1ca7-129">例如：</span><span class="sxs-lookup"><span data-stu-id="a1ca7-129">For example:</span></span>

  * <span data-ttu-id="a1ca7-130">`myregistry.azurecr.io/aspnetcore:1.0.1` 表示全公司的映像</span><span class="sxs-lookup"><span data-stu-id="a1ca7-130">`myregistry.azurecr.io/aspnetcore:1.0.1` represents a corporate-wide image</span></span>
  * <span data-ttu-id="a1ca7-131">`myregistry.azurecr.io/warrantydept/dotnet-build`代表的映像使用 toobuild.NET 應用程式，請在 hello 擔保部門之間共用</span><span class="sxs-lookup"><span data-stu-id="a1ca7-131">`myregistry.azurecr.io/warrantydept/dotnet-build` represents an image used toobuild .NET apps, shared across hello warranty department</span></span>
  * <span data-ttu-id="a1ca7-132">`myregistry.azrecr.io/warrantydept/customersubmissions/web`代表 web 映像，分組在 hello 客戶提交應用程式中的 hello 擔保部門所擁有</span><span class="sxs-lookup"><span data-stu-id="a1ca7-132">`myregistry.azrecr.io/warrantydept/customersubmissions/web` represents a web image, grouped in hello customer submissions app, owned by hello warranty department</span></span>

* <span data-ttu-id="a1ca7-133">**映像** - 儲存在儲存機制中，每個映像是 Docker 容器的唯讀快照。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-133">**Image** - Stored in a repository, each image is a read-only snapshot of a Docker container.</span></span> <span data-ttu-id="a1ca7-134">Azure 容器登錄庫可以包含 Windows 和 Linux 映像。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-134">Azure container registries can include both Windows and Linux images.</span></span> <span data-ttu-id="a1ca7-135">您可以控制您的所有容器部署的映像名稱。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-135">You control image names for all your container deployments.</span></span> <span data-ttu-id="a1ca7-136">使用標準[Docker 命令](https://docs.docker.com/engine/reference/commandline/)toopush 映像儲存機制，或提取從儲存機制的映像。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-136">Use standard [Docker commands](https://docs.docker.com/engine/reference/commandline/) toopush images into a repository, or pull an image from a repository.</span></span>

* <span data-ttu-id="a1ca7-137">**容器** - 容器定義軟體應用程式及其相依性，包裹在完整的檔案系統中，包括程式碼、執行階段、系統工具和程式庫。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-137">**Container** - A container defines a software application and its dependencies wrapped in a complete filesystem including code, runtime, system tools, and libraries.</span></span> <span data-ttu-id="a1ca7-138">根據您從容器登錄庫提取的 Windows 或 Linux 映像，執行 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-138">Run Docker containers based on Windows or Linux images that you pull from a container registry.</span></span> <span data-ttu-id="a1ca7-139">在單一機器上執行的容器共用 hello 作業系統核心。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-139">Containers running on a single machine share hello operating system kernel.</span></span> <span data-ttu-id="a1ca7-140">Docker 容器是完全可攜 tooall 主要 Linux 散發版本、 Mac 和 Windows。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-140">Docker containers are fully portable tooall major Linux distros, Mac, and Windows.</span></span>




## <a name="next-steps"></a><span data-ttu-id="a1ca7-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1ca7-141">Next steps</span></span>
* [<span data-ttu-id="a1ca7-142">建立容器登錄中使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a1ca7-142">Create a container registry using hello Azure portal</span></span>](container-registry-get-started-portal.md)
* [<span data-ttu-id="a1ca7-143">建立容器登錄中使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="a1ca7-143">Create a container registry using hello Azure CLI</span></span>](container-registry-get-started-azure-cli.md)
* [<span data-ttu-id="a1ca7-144">推入第一個映像使用 Docker CLI hello</span><span class="sxs-lookup"><span data-stu-id="a1ca7-144">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
* <span data-ttu-id="a1ca7-145">toobuild 連續整合和部署工作流程使用 Visual Studio Team Services、 Azure 容器服務，以及 Azure 容器登錄中，請參閱[本教學課程](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-145">toobuild a continuous integration and deployment workflow using Visual Studio Team Services, Azure Container Service, and Azure Container Registry, see [this tutorial](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).</span></span>
* <span data-ttu-id="a1ca7-146">如果要 tooset 自己 Docker 私人登錄在 Azure 中 （不含公用端點），請參閱[部署您自己私用 Docker 登錄在 Azure 上](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md)。</span><span class="sxs-lookup"><span data-stu-id="a1ca7-146">If you want tooset up your own Docker private registry in Azure (without a public endpoint), see [Deploying Your Own Private Docker Registry on Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).</span></span>
