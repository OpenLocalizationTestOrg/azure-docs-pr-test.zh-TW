---
title: "aaaAzure 容器登錄儲存機制 |Microsoft 文件"
description: "如何針對 Docker 映像 toouse Azure 容器登錄中儲存機制"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: cristyg
ms.openlocfilehash: 108622c565e41777fbb1fc9da9a01168abc7a7fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a><span data-ttu-id="69e85-103">Azure 容器登錄存放庫</span><span class="sxs-lookup"><span data-stu-id="69e85-103">Azure container registry repositories</span></span>

<span data-ttu-id="69e85-104">Azure 容器登錄中，可讓您在儲存機制中 toostore 容器映像。</span><span class="sxs-lookup"><span data-stu-id="69e85-104">Azure container registry allows you toostore container images in repositories.</span></span> <span data-ttu-id="69e85-105">透過將映像儲存在存放庫中，您可以在隔離的環境中擁有映像 (或映像的版本) 的群組。</span><span class="sxs-lookup"><span data-stu-id="69e85-105">By storing images in repositories, you can have groups of images (or version of images) in isolated environments.</span></span> <span data-ttu-id="69e85-106">推送映像 tooyour 登錄時，您可以指定這些儲存機制。</span><span class="sxs-lookup"><span data-stu-id="69e85-106">You can specify these repositories when you push images tooyour registry.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="69e85-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="69e85-107">Prerequisites</span></span>
* <span data-ttu-id="69e85-108">**Azure 容器登錄庫** - 在 Azure 訂用帳戶中建立容器登錄庫。</span><span class="sxs-lookup"><span data-stu-id="69e85-108">**Azure container registry** - Create a container registry in your Azure subscription.</span></span> <span data-ttu-id="69e85-109">例如，使用 hello [Azure 入口網站](container-registry-get-started-portal.md)或 hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="69e85-109">For example, use hello [Azure portal](container-registry-get-started-portal.md) or hello [Azure CLI 2.0](container-registry-get-started-azure-cli.md).</span></span>
* <span data-ttu-id="69e85-110">**Docker CLI** -tooset Docker 主機和存取 hello Docker CLI 命令，在本機電腦上的安裝[Docker 引擎](https://docs.docker.com/engine/installation/)。</span><span class="sxs-lookup"><span data-stu-id="69e85-110">**Docker CLI** - tooset up your local computer as a Docker host and access hello Docker CLI commands, install [Docker Engine](https://docs.docker.com/engine/installation/).</span></span>
* <span data-ttu-id="69e85-111">**提取映像**-從 hello 公用 Docker Hub 登錄提取映像、 標記，並將它推送 tooyour 登錄。</span><span class="sxs-lookup"><span data-stu-id="69e85-111">**Pull an image** - Pull an image from hello public Docker Hub registry, tag it, and push it tooyour registry.</span></span> <span data-ttu-id="69e85-112">如需如何指引發送和提取映像，請參閱[推入 Docker 映像 tooAzure 私人登錄](container-registry-get-started-docker-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="69e85-112">For guidance on how push and pull images, see [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md).</span></span>


## <a name="viewing-repositories-in-hello-portal"></a><span data-ttu-id="69e85-113">在 hello 入口網站中檢視儲存機制</span><span class="sxs-lookup"><span data-stu-id="69e85-113">Viewing repositories in hello Portal</span></span>

<span data-ttu-id="69e85-114">一旦您已推入映像 tooyour 容器登錄中，您可以看到 hello 儲存機制裝載在 hello Azure 入口網站中的 hello 映像的清單。</span><span class="sxs-lookup"><span data-stu-id="69e85-114">Once you have pushed images tooyour container registry, you can see a list of hello repositories hosting hello images in hello Azure portal.</span></span>

<span data-ttu-id="69e85-115">如果您遵循 hello 中的 hello 步驟[推入 Docker 映像 tooAzure 私人登錄](container-registry-get-started-docker-cli.md)發行項，您現在應該有 Nginx 映像，在容器登錄中。</span><span class="sxs-lookup"><span data-stu-id="69e85-115">If you followed hello steps in hello [Push Docker image tooAzure private registry](container-registry-get-started-docker-cli.md) article, you should now have a Nginx image in your container registry.</span></span> <span data-ttu-id="69e85-116">Hello 指示的一部分，您應該指定 hello 映像的命名空間。</span><span class="sxs-lookup"><span data-stu-id="69e85-116">As part of hello instructions, you should have specified a namespace for hello image.</span></span> <span data-ttu-id="69e85-117">Hello 以下範例中的 hello 命令將推送 hello NGinx 映像 toohello"samples"儲存機制：</span><span class="sxs-lookup"><span data-stu-id="69e85-117">In hello example below, hello command pushes hello NGinx image toohello "samples" repository:</span></span>

```
docker push myregistry.azurecr.io/samples/nginx
```
 <span data-ttu-id="69e85-118">Azure 容器登錄庫支援多層級的儲存機制命名空間。</span><span class="sxs-lookup"><span data-stu-id="69e85-118">Azure Container Registry supports multilevel repository namespaces.</span></span> <span data-ttu-id="69e85-119">這項功能可讓您 toogroup 集合的映像相關的 tooa 特定應用程式或應用程式 toospecific 開發或操作團隊的集合。</span><span class="sxs-lookup"><span data-stu-id="69e85-119">This feature enables you toogroup collections of images related tooa specific app, or a collection of apps toospecific development or operational teams.</span></span> <span data-ttu-id="69e85-120">tooread 有關容器登錄中的儲存機制的詳細資訊請參閱[在 Azure 中的私用 Docker 容器登錄](container-registry-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="69e85-120">tooread more about repositories in container registries, see [Private Docker container registries in Azure](container-registry-intro.md).</span></span>

<span data-ttu-id="69e85-121">tooview hello 容器登錄儲存機制：</span><span class="sxs-lookup"><span data-stu-id="69e85-121">tooview hello container registry repositories:</span></span>

1. <span data-ttu-id="69e85-122">登入 toohello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="69e85-122">Log in toohello Azure portal</span></span>
2. <span data-ttu-id="69e85-123">在 hello **Azure 容器登錄中**刀鋒視窗中，您想 tooinspect 選取 hello 登錄</span><span class="sxs-lookup"><span data-stu-id="69e85-123">On hello **Azure Container Registry** blade, select hello registry you wish tooinspect</span></span>
3. <span data-ttu-id="69e85-124">在 hello 登錄刀鋒視窗中，按一下 **儲存機制**toosee 所有 hello 儲存機制和其映像的清單</span><span class="sxs-lookup"><span data-stu-id="69e85-124">In hello registry blade, click **Repositories** toosee a list of all hello repositories and their images</span></span>
4. <span data-ttu-id="69e85-125">（選擇性）選取特定的映像 toosee 標記</span><span class="sxs-lookup"><span data-stu-id="69e85-125">(Optional) Select a specific image toosee tags</span></span>

![Hello 入口網站中的儲存機制](./media/container-registry-repositories/container-registry-repositories.png)


## <a name="next-steps"></a><span data-ttu-id="69e85-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69e85-127">Next steps</span></span>
<span data-ttu-id="69e85-128">知道 hello 基本概念之後，您已經準備好使用您的登錄的 toostart ！</span><span class="sxs-lookup"><span data-stu-id="69e85-128">Now that you know hello basics, you are ready toostart using your registry!</span></span> <span data-ttu-id="69e85-129">例如，啟動 部署容器映像 tooan [Azure 容器服務](https://azure.microsoft.com/documentation/services/container-service/)叢集。</span><span class="sxs-lookup"><span data-stu-id="69e85-129">For example, start deploying container images tooan [Azure Container Service](https://azure.microsoft.com/documentation/services/container-service/) cluster.</span></span>
